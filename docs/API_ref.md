# API References

## volumesnapshotbackups.datamover.oadp.openshift.io

```
KIND:     VolumeSnapshotBackup
VERSION:  datamover.oadp.openshift.io/v1alpha1

DESCRIPTION:
     VolumeSnapshotBackup is the Schema for the volumesnapshotbackups API

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     VolumeSnapshotBackupSpec defines the desired state of VolumeSnapshotBackup

   status	<Object>
     VolumeSnapshotBackupStatus defines the observed state of
     VolumeSnapshotBackup

```


## volumesnapshotrestores.datamover.oadp.openshift.io

```
KIND:     VolumeSnapshotRestore
VERSION:  datamover.oadp.openshift.io/v1alpha1

DESCRIPTION:
     VolumeSnapshotRestore is the Schema for the volumesnapshotrestores API

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     VolumeSnapshotRestoreSpec defines the desired state of
     VolumeSnapshotRestore

   status	<Object>
     VolumeSnapshotRestoreStatus defines the observed state of
     VolumeSnapshotRestore

```


## cloudstorages.oadp.openshift.io

```
KIND:     CloudStorage
VERSION:  oadp.openshift.io/v1alpha1

DESCRIPTION:
     <empty>

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>

   status	<Object>

```


## dataprotectionapplications.oadp.openshift.io

```
KIND:     DataProtectionApplication
VERSION:  oadp.openshift.io/v1alpha1

DESCRIPTION:
     DataProtectionApplication is the Schema for the dpa API

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     DataProtectionApplicationSpec defines the desired state of Velero

   status	<Object>
     DataProtectionApplicationStatus defines the observed state of
     DataProtectionApplication

```


## backuprepositories.velero.io

```
KIND:     BackupRepository
VERSION:  velero.io/v1

DESCRIPTION:
     <empty>

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     BackupRepositorySpec is the specification for a BackupRepository.

   status	<Object>
     BackupRepositoryStatus is the current status of a BackupRepository.

```


## backupstoragelocations.velero.io

```
KIND:     BackupStorageLocation
VERSION:  velero.io/v1

DESCRIPTION:
     BackupStorageLocation is a location where Velero stores backup objects

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     BackupStorageLocationSpec defines the desired state of a Velero
     BackupStorageLocation

   status	<Object>
     BackupStorageLocationStatus defines the observed state of
     BackupStorageLocation

```


## backups.velero.io

```
KIND:     Backup
VERSION:  velero.io/v1

DESCRIPTION:
     Backup is a Velero resource that represents the capture of Kubernetes
     cluster state at a point in time (API objects and associated volume state).

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     BackupSpec defines the specification for a Velero backup.

   status	<Object>
     BackupStatus captures the current status of a Velero backup.

```


## deletebackuprequests.velero.io

```
KIND:     DeleteBackupRequest
VERSION:  velero.io/v1

DESCRIPTION:
     DeleteBackupRequest is a request to delete one or more backups.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     DeleteBackupRequestSpec is the specification for which backups to delete.

   status	<Object>
     DeleteBackupRequestStatus is the current status of a DeleteBackupRequest.

```


## downloadrequests.velero.io

```
KIND:     DownloadRequest
VERSION:  velero.io/v1

DESCRIPTION:
     DownloadRequest is a request to download an artifact from backup object
     storage, such as a backup log file.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     DownloadRequestSpec is the specification for a download request.

   status	<Object>
     DownloadRequestStatus is the current status of a DownloadRequest.

```


## podvolumebackups.velero.io

```
KIND:     PodVolumeBackup
VERSION:  velero.io/v1

DESCRIPTION:
     <empty>

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     PodVolumeBackupSpec is the specification for a PodVolumeBackup.

   status	<Object>
     PodVolumeBackupStatus is the current status of a PodVolumeBackup.

```


## podvolumerestores.velero.io

```
KIND:     PodVolumeRestore
VERSION:  velero.io/v1

DESCRIPTION:
     <empty>

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     PodVolumeRestoreSpec is the specification for a PodVolumeRestore.

   status	<Object>
     PodVolumeRestoreStatus is the current status of a PodVolumeRestore.

```


## restores.velero.io

```
KIND:     Restore
VERSION:  velero.io/v1

DESCRIPTION:
     Restore is a Velero resource that represents the application of resources
     from a Velero backup to a target Kubernetes cluster.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     RestoreSpec defines the specification for a Velero restore.

   status	<Object>
     RestoreStatus captures the current status of a Velero restore

```


## schedules.velero.io

```
KIND:     Schedule
VERSION:  velero.io/v1

DESCRIPTION:
     Schedule is a Velero resource that represents a pre-scheduled or periodic
     Backup that should be run.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     ScheduleSpec defines the specification for a Velero schedule

   status	<Object>
     ScheduleStatus captures the current state of a Velero schedule

```


## serverstatusrequests.velero.io

```
KIND:     ServerStatusRequest
VERSION:  velero.io/v1

DESCRIPTION:
     ServerStatusRequest is a request to access current status information about
     the Velero server.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<map[string]>
     ServerStatusRequestSpec is the specification for a ServerStatusRequest.

   status	<Object>
     ServerStatusRequestStatus is the current status of a ServerStatusRequest.

```


## volumesnapshotlocations.velero.io

```
KIND:     VolumeSnapshotLocation
VERSION:  velero.io/v1

DESCRIPTION:
     VolumeSnapshotLocation is a location where Velero stores volume snapshots.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     VolumeSnapshotLocationSpec defines the specification for a Velero
     VolumeSnapshotLocation.

   status	<Object>
     VolumeSnapshotLocationStatus describes the current status of a Velero
     VolumeSnapshotLocation.

```

## how to generate this file 

From the oadp-operator git repo, execute:
```
clear; for i in `ls bundle/manifests/*oadp.openshift.io* bundle/manifests/velero.io* | xargs -I {} sh -c 'yq ".metadata.name" {}'`; do printf "${bold}## $i${normal}\n\n"; printf "\`\`\`\n"; oc explain $i; printf "\`\`\`\n"; printf "\n\n"; done
```
