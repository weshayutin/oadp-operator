# How to Use VMFR (VirtualMachineFileRestore)

This guide walks you through using VirtualMachineFileRestore to recover files from VM backups.

## Prerequisites

### Data Protection Application (DPA) 
```
spec:
  backupLocations:
  - velero:
      config:
        profile: default
        region: us-west-2
      credential:
        key: cloud
        name: cloud-credentials
      default: true
      objectStorage:
        bucket: cvpbucfoo2
        prefix: velero
      provider: aws
  configuration:
    nodeAgent:
      enable: true
      uploaderType: kopia
    velero:
      defaultPlugins:
      - kubevirt
      - csi
      - openshift
      - aws
      - hypershift
      disableFsBackup: false
      logLevel: debug
  logFormat: text
  nonAdmin:
    enable: false
  vmFileRestore:
    enable: true
```

### CNV Installation

Ensure CNV (Container-native Virtualization) is installed and running:

- Verify you can launch a VM
- Confirm you have a default storage class configured
```
 oc get sc
NAME                                         PROVISIONER                             RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
local-block-hpp                              kubernetes.io/no-provisioner            Delete          WaitForFirstConsumer   false                  122m
local-block-ocs                              kubernetes.io/no-provisioner            Delete          WaitForFirstConsumer   false                  122m
nfs                                          kubernetes.io/no-provisioner            Delete          Immediate              false                  114m
ocs-storagecluster-ceph-rbd (default)        openshift-storage.rbd.csi.ceph.com      Delete          Immediate              true                   112m
ocs-storagecluster-ceph-rbd-virtualization   openshift-storage.rbd.csi.ceph.com      Delete          Immediate              true                   95m
ocs-storagecluster-ceph-rgw                  openshift-storage.ceph.rook.io/bucket   Delete          Immediate              false                  117m
ocs-storagecluster-cephfs                    openshift-storage.cephfs.csi.ceph.com   Delete          Immediate              true                   112m
standard-csi                                 cinder.csi.openstack.org                Delete          WaitForFirstConsumer   true                   154m
```

## VM Setup

Create a namespace for the test VMs:
```
oc create namespace cirros-test-cont
```

Deploy the test VMs:

```
oc create -f cirros-test-1.yaml -f cirros-test-2.yaml -f cirros-test-3.yaml 
```

## Backup Process

### Step 1: Add Files to VMs

1. Access the running Cirros VMs via the OpenShift console
2. Add directories and files as needed for your test scenario

### Step 2: Create Initial Backup
```
oc oadp backup create vmtest1 --snapshot-move-data=true --include-namespaces=cirros-test-cont
```

### Step 3: Add More Files

Add additional files to your VMs as desired for testing multiple backup points.

### Step 4: Create Second Backup

```
oc oadp backup create vmtest2 --snapshot-move-data=true --include-namespaces=cirros-test-cont
```

## VM Backup Discovery and File Recovery

> **Important:** From this point forward, all custom resources (CRs) must be created in the protected namespace (by default `openshift-adp`).

### Step 1: Create a Secret for VMFR Access

Create a secret containing credentials for accessing the file browser:

```
apiVersion: v1
data:
  password: dGhpc3Bhc3N3MHJkaXNtb3JldGhhbnR3ZWx2ZWNoYXJhdGVycw==
  username: d2hheXV0aW5AcmVkaGF0LmNvbQ==
kind: Secret
metadata:
  name: vmfrsecret1
  namespace: openshift-adp
type: Opaque

```

### Step 2: Create a VM Backup Discovery Object

This object will discover all backups containing the specified VM name based on your search criteria:

```
apiVersion: oadp.openshift.io/v1alpha1
kind: VirtualMachineBackupsDiscovery
metadata:
  name: vmbdtest-oadp1
  # need doc, spec to note this has to be the protected namespace
  namespace: openshift-adp
spec:
  virtualMachineName: cirros-test-cont-1
  virtualMachineNamespace: cirros-test-cont
```

**Expected Results:**

After creating the discovery object, you should see output similar to the following:

```
apiVersion: oadp.openshift.io/v1alpha1
kind: VirtualMachineBackupsDiscovery
metadata:
  creationTimestamp: "2025-12-12T16:00:47Z"
  generation: 1
  name: vmbdtest-oadp1
  namespace: openshift-adp
  resourceVersion: "85120"
  uid: 425542fa-d5e6-4d0a-b837-758ebca044d8
spec:
  virtualMachineName: cirros-test-cont-1
  virtualMachineNamespace: cirros-test-cont
status:
  backupDiscoveryProgress:
  - createdAt: "2025-12-12T16:00:16Z"
    lastUpdated: "2025-12-12T16:00:47Z"
    message: VM found in backup
    name: vmtest3
    namespace: openshift-adp
    status: Completed
  - createdAt: "2025-12-12T15:58:36Z"
    lastUpdated: "2025-12-12T16:00:47Z"
    message: VM found in backup
    name: vmtest2
    namespace: openshift-adp
    status: Completed
  - createdAt: "2025-12-12T15:56:46Z"
    lastUpdated: "2025-12-12T16:00:47Z"
    message: VM found in backup
    name: vmtest1
    namespace: openshift-adp
    status: Completed
  conditions:
  - lastTransitionTime: "2025-12-12T16:00:47Z"
    message: Successfully discovered 3 valid backups
    reason: DiscoverySuccessful
    status: "True"
    type: Ready
  discoveryStats:
    completed: 3
    completionTime: "2025-12-12T16:00:47Z"
    failed: 0
    inProgress: 0
    pending: 0
    skipped: 0
    startTime: "2025-12-12T16:00:47Z"
    totalCandidates: 3
  observedGeneration: 1
  phase: Completed
  validBackups:
  - createdAt: "2025-12-12T16:00:16Z"
    name: vmtest3
    namespace: openshift-adp
  - createdAt: "2025-12-12T15:58:36Z"
    name: vmtest2
    namespace: openshift-adp
  - createdAt: "2025-12-12T15:56:46Z"
    name: vmtest1
    namespace: openshift-adp
```

> **Note:** In this example, three valid backups were found for the specified VM.

### Step 3: Create the VM File Restore Instance

Create a VirtualMachineFileRestore object to restore files from the discovered backups:

```
apiVersion: oadp.openshift.io/v1alpha1
kind: VirtualMachineFileRestore
metadata:
  name: vmfrtest-oadp3
  # must use openshift-adp or protected namespace
  namespace: openshift-adp
spec:
  backupsDiscoveryRef: vmbdtest-oadp1
  fileAccess:
    fileBrowser:
      # password must be at least 12 characters long
      credentialsSecretRef:
        name: vmfrsecret1
      exposeExternally: true
  selectedBackups:
  - vmtest1
  - vmtest2
  - vmtest3
```

> **Note:** This will create Velero restore operations for each backup listed in the `selectedBackups` field.

**Expected Results:**

After creating the file restore instance, you should see output similar to the following:

```
apiVersion: oadp.openshift.io/v1alpha1
kind: VirtualMachineFileRestore
metadata:
  creationTimestamp: "2025-12-12T16:36:49Z"
  finalizers:
  - oadp.openshift.io/velero-restore-cleanup-finalizer
  - oadp.openshift.io/vm-file-restore-finalizer
  generation: 1
  name: vmfrtest-oadp3
  namespace: openshift-adp
  resourceVersion: "119146"
  uid: 3ade9702-36a9-4604-b389-82ebde107eed
spec:
  backupsDiscoveryRef: vmbdtest-oadp1
  fileAccess:
    fileBrowser:
      credentialsSecretRef:
        name: vmfrsecret1
      exposeExternally: true
  selectedBackups:
  - vmtest1
  - vmtest2
  - vmtest3
status:
  conditions:
  - lastTransitionTime: "2025-12-12T16:37:36Z"
    message: File server and external route are ready
    reason: FileServerCreated
    status: "False"
    type: Progressing
  - lastTransitionTime: "2025-12-12T16:37:36Z"
    message: File server is accessible and serving files
    reason: FileServerAvailable
    status: "True"
    type: Available
  - lastTransitionTime: "2025-12-12T16:36:49Z"
    message: All operations completed successfully
    reason: NoFailures
    status: "False"
    type: Degraded
  - lastTransitionTime: "2025-12-12T16:37:36Z"
    message: File restore completed, files accessible via file server and external
      route
    reason: Completed
    status: "True"
    type: Ready
  createdNamespace: cirros-test-cont-cirros-test-cont-1-3ade9702
  fileServingInfo:
    fileBrowser:
      clusterAccess: https://vmfrtest-oadp3-fileserver-svc.cirros-test-cont-cirros-test-cont-1-3ade9702.svc.cluster.local:8443
      credentialsSecretRef:
        name: vmfrtest-oadp3-filebrowser-zthbh
        namespace: cirros-test-cont-cirros-test-cont-1-3ade9702
      publicAccess: https://vmfrtest-oadp3.vmfr.apps.migvmfr1012.rhos-psi.cnv-qe.rhood.us
  observedGeneration: 1
  phase: Completed
  pvcRestores:
  - pvcName: cirros-test-cont-1-dv
    pvcNamespace: cirros-test-cont
    pvcUID: 05ac1521-2a16-4a71-b81f-ccad592b89cd
    restores:
    - phase: Completed
      state: available
      timestamp: "2025-12-12T16:00:16Z"
      veleroBackupName: vmtest3
      veleroBackupNamespace: openshift-adp
      veleroRestoreName: vmfr-vmfrtest-oadp3-vmtest3-89lfl
      veleroRestoreNamespace: openshift-adp
    - phase: Completed
      state: available
      timestamp: "2025-12-12T15:58:36Z"
      veleroBackupName: vmtest2
      veleroBackupNamespace: openshift-adp
      veleroRestoreName: vmfr-vmfrtest-oadp3-vmtest2-bfqx4
      veleroRestoreNamespace: openshift-adp
    - phase: Completed
      state: available
      timestamp: "2025-12-12T15:56:46Z"
      veleroBackupName: vmtest1
      veleroBackupNamespace: openshift-adp
      veleroRestoreName: vmfr-vmfrtest-oadp3-vmtest1-vpzds
      veleroRestoreNamespace: openshift-adp
    size: 150Mi

```

## Accessing and Downloading Files

Once the file restore is complete, you can access the files through the file browser:

1. **Navigate to the URL:** Use the `publicAccess` URL from the `fileServingInfo.fileBrowser` section in the status output above
2. **Login:** Use the credentials you specified in the secret (`vmfrsecret1`)
3. **Browse Files:** Use the file browser UI to search for and locate the files you need
4. **Download:** Select and download the desired files

> **Note:** The password in the secret must be at least 12 characters long. 
