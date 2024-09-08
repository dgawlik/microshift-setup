
# Installing RHEL-9

Go to https://developers.redhat.com/products/rhel/overview

Click download RHEL at no cost

Go to https://console.redhat.com/openshift

Go to downloads:

Click download Pull Secret

Run virt-manager, create new machine

Select downloaded image, give it 2 core, 4096MB ram and 100GM disk

Follow through the installation

Register os with your developers email and password

create root password

IMPORTANT! to enable sharing with host select in software packages 'virtualization client'

On Host create share file with Fat32 filesystem

dd if=/dev/zero of=fat32.img bs=1M count=1000

mkfs.vfat fat32.img

Mount file in folder with loopback device

mkdir share

sudo mount -t vfat -o loop,uid=1000,gid=1000 fat32.img share

virsh attach-disk rhel9-ocp fat32.img vdb --targetbus virtio --persistent

In guest mount the disk

sudo mount -t vfat /dev/vdb /mnt/share