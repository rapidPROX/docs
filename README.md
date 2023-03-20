# rapidPROX Documentation
## User and developer documentation

The rapidPROX framework consists of ...
1. A dpdk application that can be configured as a traffic generator or as a packet processing workload.
2. Traffic profiles can support L2/L3 flows capable of saturating 100 Gbps (and up) interfaces using COTS server platforms and standard high volume NICs.
3. rapidPROX workloads can be confgured to represent various packet handling functions, for exmaple classify, drop, Forward, encap/decap, load balance based on packet fields, Symmetric load balancing, ARP, QoS, Routing, ACL, etc.
4. A controller for automation which includes configuring workloads, executing tests and collecting statistics and performance data rom the generator and workload. Results can be displayed in a terminal, written to a file or stored in remote databases using webhooks and yaml.

