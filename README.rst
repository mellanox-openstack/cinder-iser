openstack(grizzly) - add iSER (iSCSI over RDMA) support to Cinder
========================================================

This can allow 5x faster bandwidth compared to using iSCSI TCP.

For example, over RAM device LUN I got ~1.3GBps Vs. ~5.5GBps (TCP Vs. iSER), and much lower CPU overhead.



For more details, please refer to the following link: https://wiki.openstack.org/wiki/Mellanox-Cinder
