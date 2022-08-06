This is about libvirt, virsh...

Sources :
https://blog.scottlowe.org/2012/11/07/using-vlans-with-ovs-and-libvirt/


# Dependencies(must)

I've found out that installing these deps will get rid of a bunch of error messages like :

```bash
dmidecode, libvirt-storage-gluster, libvirt-storage-iscsi-direct, libvirt-storage-rbd, radvd
```


# Guest Install

The most useful options for 'virt-instal' :

```bash
	## specify the hypervisor to use :
		--connect [hypervisor URI]
		eg:
		--connect qemu:///system
		--connect qemu:///session
		--connect lxc:///
		--connect xen:///

	## guest vm name :
		--name [name]

	## add a cdrom (iso) :
		--cdrom /path/to/iso

	## automatic installation '--unattended' useful suboptions :
		admin-password-file=/path/to/passwordfile
		user-login=
		user-password-file=/path/to/passwordfile
		product-key= #for windows guests

		eg :
		virt-install --cdrom /path/to/win.iso --unattended

	## '--boot' suboptions :
		cdrom,fd,hd,netowrk # cd,first floppy, first hdd, pxe
		kernel=[kernel],inird=[initrd],kernel_args=["arg1 arg2..."]
		bootmenu.enable=[on/off]
		uefi

	## '--os-variant' for guest type :
		--os-variant=[auto||none||win10...]
		# for the full list run
		osinfo-query os

	## '--disk' for guest storage, useful suboptions :
		path /path/to/storage.qcow2
		# if it doesn't exist libvirt will try to create it, require :
		size=[in GiB]
		sparse=[yes||no] # thinprovioned disk
		format=[qcow2||raw||vmdk...]
		device=[cdrom||disk||floppy||lun]
		boot.order=[1||2...] # lower value higher priority
		target.bus=[ide||stata||scsi||usb||virtio||xen]
		readonly=[on||off]
		driver.discard=[unmap||ignore]
		snapshot= # https://libvirt.org/formatdomain.html#elementsDisks

	## '--network' for networking, useful suboptions :
		# start with one of the following 5 :
		[  bridge=[bridge] # to bridge 'bridge'
		|| network=[netname] # to network already made with 'virsh'
		|| type=direct,source=[iface],source.mode=[bridge||vepa||private||passthrough] # to macvtap@iface
		|| user # to SLIRP qemu network (NAT)
		|| none # no net iface at all
		]

		model=[e1000 || virtio || rtl8139...]
		mac=[macaddress]
		virtualport. #'virt-install "--network=?"for info, no --mac, --bridge,--nonenetwork with this

	## video devices (gpu) :
		--video [virtio || cirrus || vga || qxl || vmvga]
		# https://libvirt.org/formatdomain.html#elementsVideo

	## '--graphics' only how to access the guest, no hardware (no need to use this option normally) :
		[vnc || spice || none]

	## virtualization options :
		--hvm # qemu full virtualization
		--paravirt # paravirtualized guest
		--virt-type [kvm,qemu,xen...]

	## sound options :
		--sound [default || ich9 || ac97...]

	## pci passthrough '--hostdev' :
		--hostdev [ use '(lsusb || lspci || virsh nodedev-list)' to get the device bus ]

	## memory ballooning (inflating an deflating guest memory when needed) :
		--memballoon [virtio || xen || none]

	## tpm device :
		--tmp [emulator || /path/to/tpm]
	## random number generator :
		--rng [random || egd || builtin]
		# 'random' needed suboptions:
		backend -> /dev/random
		'--rng /dev/random'

	## get the vm xml without creating it (still create the storage, use --dry-run if no) :
		--print-xml

```

## Examples:
E.g 1:
	virt-install --connect qemu://system --arch=x86_64 --name vmname --memory 1024 \
	--cpu host --vcpus=1 --disk path=/var/lib/libvirt/images/vmname.img,size=20 \
	--network bridge=br0 \
	--cdrom /var/lib/libvirt/images/os-install.iso \
	--graphics vnc --noautoconsole --hvm \
	--os-variant win2k3
E.g 2:
	virt-install \
	--connect qemu:///system \
	--name my-win10-vm \
	--memory 4096 \
	--disk size=40 \
	--os-variant win10 \
	--cdrom /path/to/my/win10.iso

# virsh

## Networking

```bash
# add interface to guest
attach-interface

# link up or down ?
domif-getlink --domain [domname] --interface [ifacename]

# set interface up or down temporarily or persistently
domif-setlink --domain [domname] --interface [mac] --state [up|down] --persistent
domif-setlink --domain [domname] --interface [mac] --state [up|down]

```

# Openvswitch vlan xml

## creating openvswitch netowrk with vlans : (example)

<network>
  <name>ovs-network</name>
  <forward mode='bridge'/>
  <bridge name='ovsbr0'/>
  <virtualport type='openvswitch'/>
  <portgroup name='vlan-01' default='yes'>
  </portgroup>
  <portgroup name='vlan-02'>
    <vlan>
      <tag id='2'/>
    </vlan>
  </portgroup>
  <portgroup name='vlan-03'>
    <vlan>
      <tag id='3'/>
    </vlan>
  </portgroup>
  <portgroup name='vlan-all'>
    <vlan trunk='yes'>
      <tag id='2'/>
      <tag id='3'/>
    </vlan>
  </portgroup>
</network>

## attaching domains "vms" to the vlans :

<interface type='network'>
  <target dev='ifacename'/> # set port name on switch, eg: kali guest dev='kali0'
  <mac address='11:22:33:44:55:66'/>
  <source network='ovs-network' portgroup='vlan-02'/>
</interface>
