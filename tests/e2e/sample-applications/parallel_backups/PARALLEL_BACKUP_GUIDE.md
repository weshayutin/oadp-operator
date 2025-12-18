# Parallel Backup and Node Agent Concurrency in OADP

This guide explains the parallel backup capabilities in OADP (OpenShift API for Data Protection) and Velero, specifically focusing on Node Agent concurrency for data movement. This allows you to perform backups of multiple namespaces and persistent volumes simultaneously, significantly reducing the total backup window.

## Overview

By default, backup operations might be limited by configuration to ensure system stability. However, OADP allows you to tune these settings to maximize throughput, especially when using **Data Mover** features (moving snapshot data to object storage via the Node Agent).

The "Parallel Backup" setup in this directory demonstrates:
1.  **Multiple Namespaces**: Four isolated namespaces (`namespace1` - `namespace4`) each running a MySQL application with a Persistent Volume.
2.  **Concurrent Processing**: Configuring the OADP Node Agent to process multiple volumes in parallel.
3.  **Simultaneous Backup Requests**: Submitting multiple Backup Custom Resources (CRs) at once to trigger parallel execution.

## 1. Environment Setup

We have prepared four identical namespaces, each containing:
*   **MySQL Deployment**: A stateful application.
*   **PersistentVolumeClaim (PVC)**: 1Gi storage using `gp2-csi`.
*   **Service/Route**: Network access.

The resource files are organized as follows:
*   `namespace1/`
*   `namespace2/`
*   `namespace3/`
*   `namespace4/`

To deploy these workloads:
```bash
for i in {1..4}; do oc create -f namespace$i/; done
# Ensure PVCs are bound and Pods are running
```

## 2. OADP Configuration: Node Agent Concurrency

To enable parallel data movement (uploading volume data to object storage), we configure the `DataProtectionApplication` (DPA). The key setting is `loadConcurrency` under the `nodeAgent` configuration.

### Example Configuration (`dpa-node-agent-concurrency.yaml`)

This configuration sets the global concurrency limit for the Node Agent to **4**. This means the Node Agent can process up to 4 volume uploads simultaneously per node (or globally depending on specific scheduling).

```yaml
apiVersion: oadp.openshift.io/v1alpha1
kind: DataProtectionApplication
metadata:
  name: dpa-sample
  namespace: openshift-adp
spec:
  # ... (BackupLocation and SnapshotLocation config) ...
  configuration:
    nodeAgent:
      enable: true
      uploaderType: kopia
      loadConcurrency:
        globalConfig: 4  # <--- Allows 4 concurrent data moves
```

Apply this configuration to your cluster to update the Node Agent settings.

## 3. The Backup Specifications

We have created four separate Backup CRs, one for each namespace. Each backup is configured to use the data mover (`snapshotMoveData: true`).

*   `backup-namespace1.yaml`
*   `backup-namespace2.yaml`
*   `backup-namespace3.yaml`
*   `backup-namespace4.yaml`

**Key Spec Attributes:**
```yaml
spec:
  includedNamespaces:
  - namespaceX
  snapshotMoveData: true  # Triggers the Node Agent data movement
  storageLocation: dpa-sample-1
```

## 4. Executing Parallel Backups

To test the parallel capability, submit all four backup requests simultaneously:

```bash
oc create -f backup-namespace1.yaml
oc create -f backup-namespace2.yaml
oc create -f backup-namespace3.yaml
oc create -f backup-namespace4.yaml
```

## 5. Verifying Parallel Execution

You can observe the parallel processing by checking the status of the backups and the logs of the Node Agent pods.

1.  **Watch Backup Status**:
    ```bash
    watch "oc get backups -n openshift-adp"
    ```
    You should see multiple backups in `InProgress` state simultaneously.

2.  **Check Data Uploads**:
    When `snapshotMoveData` is true, Velero creates `DataUpload` (or `PodVolumeBackup` in older versions) resources.
    ```bash
    oc get datauploads -n openshift-adp
    ```
    With the `loadConcurrency` set to 4, you should see up to 4 uploads transitioning to `InProgress` at the same time, rather than queuing one after another.

## Summary

By increasing the `loadConcurrency` in the DPA and submitting multiple backup requests, you leverage the full capacity of your infrastructure to reduce backup times for large, multi-tenant clusters.

