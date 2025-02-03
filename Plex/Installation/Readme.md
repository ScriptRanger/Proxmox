# TrueNAS ISO herunterladen
wget https://download.truenas.com/TrueNAS-ISO-latest.iso -O truenas.iso

# ISO in Proxmox als VM einbinden
qm create 100 --memory 8192 --net0 virtio,bridge=vmbr0
qm importdisk 100 truenas.iso local-lvm
qm set 100 --scsihw virtio-scsi-pci --scsi0 local-lvm:100
qm set 100 --ide2 local-lvm:cloudinit
qm set 100 --boot c --bootdisk scsi0
qm start 100
