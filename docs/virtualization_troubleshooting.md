# Troubleshooting Virtualization backup and restore

1. Create a backup for a single VM in a namespace with multiple VMs.[#create-backup-for-a-single-vm-in-a-namespace-with-multiple-vms]
1. next




## Create a backup for a single VM in a namespace with multiple VMs.

* Create the appropriate labels across the VM and VMI persistent volumes.

```
oc label pvc --all vm-name=vm-name
```

