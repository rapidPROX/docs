# rapidPROX Documentation
## Overview

There are a myriad of challenges developing a software framework that can ensure reliable and accurate KPI measurements for today's demanding Cloud based infrastructures to meet the requirements of Telco applications and Virtualized Network Functions. rapidPROX is the result of many years of collective development by virtualized networking performance and telecoms experts and delivers on these challenges. 

rapidPROX is a feature-rich software framework for testing, analysing and debugging fast-path networking infrastructures designed to run network intensive applications. It currently includes support for both VMs and container based environments. The toolset includes highly configurable and flexible traffic generator, workloads and a controller for automation of configurations, running tests and collecting results.

rapidPROX functionality includes:

1. A dpdk application configured as a traffic generator that can be run stand-alone through a command-line interface or as part of an automated framework.
2. A highly configurable dpdk application that can approximate key processing elements of a real workload.
3. Traffic profiles that can support L2 and L3 flows capable of saturating 100 Gbps (and up) using COTS server platforms and standard high volume NICs.
4. Workloads that can be confgured to represent various packet handling functions, for example classify, drop, forward, encap/decap, load balance based on packet fields, symmetric load balancing, ARP, QoS, routing, ACL, etc.
5. A controller for test automation which includes configuring workloads, executing tests and collecting statistics and performance data from both the generator and DUT.
6. Test data can be displayed in a terminal, written to a file or stored in remote databases for post processing using webhooks and yaml.

