# pci-passthrough-ryzen

followed guide: https://level1techs.com/article/ryzen-gpu-passthrough-setup-guide-fedora-26-windows-gaming-linux

win10.xml:
- place in /etc/libvirt/qemu/win10.xml
- use `virsh define /etc/libvirt/qemu/win10.xml`

NOTE: if your PC has problems loading the disk device, you may have to delete the line: `<address type='drive' controller='0' bus='0' target='0' unit='3'/>` in the <disk> block. If you started the box using virtual disk, there will be a similar line autocreated in your <vm>.xml definition that prevents the VM from creating a 'disk' device.

grub changes:
- make changes in /etc/default/grub
- `GRUB_CMDLINE_LINUX="rd.lvm.lv=fedora00/root rd.lvm.lv=fedora00/swap rd.driver.blacklist=nouveau iommu=1 amd_iommu=on rd.driver.pre=vfio-pci"`

modprobe changes:
/etc/modprobe.d/vfio.conf
`options vfio-pci ids=10de:1401,10de:0fba`


to install virtio drivers for hard drive passthrough
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/virtualization_host_configuration_and_guest_installation_guide/form-virtualization_host_configuration_and_guest_installation_guide-para_virtualized_drivers-mounting_the_image_with_virt_manager
