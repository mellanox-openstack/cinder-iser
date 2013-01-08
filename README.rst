openstack - add iSER (iSCSI over RDMA) support to Cinder
========================================================

This can allow 5x faster bandwidth compared to using iSCSI TCP.

For example, over RAM device LUN I got ~1.3GBps Vs. ~5.5GBps (TCP Vs. iSER), and much lower CPU overhead.

The tests I ran and passed: create a volume, attach to VM, detach from VM, and delete the volume.


Instructions:

Added two flags in "/etc/cinder/cinder.conf":

transport = iser (by default will be iscsi)

iser_ip_address = 192.168.20.140 (by default will be "iscsi_ip_address")


To apply the patch, replace the files under "cinder/volume":

driver.py

iscsi.py


And under "nova/virt/libvirt":

volume.py


see the patch details in "*.patch" files.
