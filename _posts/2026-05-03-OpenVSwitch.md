### Open V-SWitch
It is an open-source OpenFlow capable virtual switch that is used typically within hypervisors to interconnect virtual machines within a host and virtual machines between differnet hosts across networks.


## Openflow
OpenFlow is a protocol that allows a controller to interact with the forwarding plane of network devices, such as switches and routers. It enables the separation of the control plane from the data plane, allowing for more flexible and programmable network management.

Below types of packets between the controller and the switch are used in OpenFlow:
- Packet In
- Flow Mod
- Packet Out

Steps to configure Open vSwitch:
1. Create a bridge


```
ovs-vsctl show
```

```
ovs-appctl fdb/show mgmt
```



ovs-vsctl add-port mybride eth0


### Features
- VLAN tagging and 802.1q trunking
- standard spanning tree protocol (802.1D)
- Link aggregation control protocol (LACP) (802.3ad)
- Port mirroring (SPAN / RSPAN)
- Flow export (e.g. sFlow, NetFlow and ipfix)
- tunneling (e.g. GRE, VXLAN, IpSec, Geneve)
- QOS control



References:
- https://www.shapeblue.com/networking-kvm-for-cloudstack/
-

