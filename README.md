wip

# vfio-passthrough-notes
personal notes on replicating my virtio/passthrough with looking glass vm


## enable virtualization in bios

for intel cpus, this is either iommu or vt-d, for amd amd-vi or svm

## install 

```$ pacman -S libvirt libvirt-glib libvirt-python qemu-full virt-manager bridge-utils dnsmasq iptables-nft edk2-ovmf```

## enable iommu

``` nano /etc/default/grub```

add ```intel_iommu=on``` to ```GRUB_CMDLINE_LINUX_DEFAULT=``` entry

regenerate grub
```grub-mkconfig -o /boot/grub/grub.cfg```


## iommu ids

```#!/bin/bash
for d in /sys/kernel/iommu_groups/*/devices/*; do
  n=${d#*/iommu_groups/*}; n=${n%%/*}
  printf 'IOMMU Group %s ' "$n"
  lspci -nns "${d##*/}"
done```





