openstack
=========

This can allow 5x faster bandwidth compared to using iSCSI TCP.
For example, over RAM device LUN I got ~1.3GBps Vs. ~5.5GBps (TCP Vs. iSER), and much lower CPU overhead.

Instructions:
On the Target/Cinder side:
Added two flags in “/etc/cinder/cinder.conf”:
transport = iser (by default will be iscsi)
iser_ip_address = 192.168.20.140 (by default will be “iscsi_ip_address”)

To apply the patch, replace the files under "cinder/volume":
driver.py
iscsi.py

And under "nova/virt/libvirt":
volume.py

