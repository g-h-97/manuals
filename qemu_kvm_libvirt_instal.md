

cat /proc/cpuinfo | grep -i vm
cat /sys/module/kvm_intel/parameters/nested

echo "option kvm-intel nested=1" > /etc/modprobe.d/kvm_nested.conf

Add the following line

```
vim /etc/default/grub
intel_iommu=on
```

#Ubuntu

sudo apt-get install --download-only qemu-kvm libvirt-daemon-system

sudo useradd [USER] libvirt
sudo useradd [USER] kvm

newgrp libvirt
newgrp kvm
