openstack(grizzly) - add iSER (iSCSI over RDMA) support to Cinder
========================================================

This can allow 5x faster bandwidth compared to using iSCSI TCP.

For example, over RAM device LUN I got ~1.3GBps Vs. ~5.5GBps (TCP Vs. iSER), and much lower CPU overhead.

The tests I ran and passed: create a volume, attach to VM, detach from VM, and delete the volume.


Instructions:

In order to enable iSER, need to adjust these values at "/etc/cinder/cinder.conf":

iser_ip_address = <ipoib/roce_address>

volume_driver = cinder.volume.drivers.lvm.LVMISERDriver

the first value is required to do a "discovery" over the IB/RoCE interface from the initiator side.

the second points cinder to use the ISERDriver, instead the LVMISCSIDriver.

Also, on nova-compute side need to adjust "/etc/nova/nova.conf":

libvirt_volume_drivers = iser=nova.virt.libvirt.volume.LibvirtISERVolumeDriver


Installation:

To apply this support, replace the files under "cinder/cinder/" And "nova/nova/" Respectively.

OR apply the patches under "cinder/" And "nova/", don't forget to copy "cinder/cinder/volume/iser.py" if you choose this way.

