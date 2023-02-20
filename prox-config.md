The configuration file is divided into multiple sections, each of which is used to define some parameters and options. Sections are created using the [section name] 
syntax. The list of sections, where # represents an integer, is as follows:

[eal options]
[port #]
[variables]
[defaults]
[global]
[core #]

In each section, entries are created using the key=value syntax. Comments are created using the ; symbol: all characters from the ; symbol to the end of line are ignored.
A # symbol at the beginning of the section name comments the whole section out: all entries in the section are treated as comments and are ignored. For example:

[#core 1]
; this is a comment
parameter name=parameter value ; this entry is ignored because the section is commented out

---

[eal options]

The following parameters are supported:

-m  ; Specifies the amount of memory used. If not provided, all hugepages will be used.
-n  ; Specifies the number of memory channels. Use -n4 for latest Intel Xeon based platforms
-r  ; Specifies the number of memory ranks.
eal ; Specifies DPDK EAL extra options. Those options will be passed blindly to DPDK.

---

[port #]

DPDK ports are usually referenced by their port_id, i.e. an integer starting from 0. Using port_id in the configuration file is tedious, since the same port_id can appear
at different places (rx port, tx port, routing tables), and those ports might change (e.g. if cables are swapped). In order to make the configuration file easier to read
and modify, DPDK ports are given a name with the name= option. The name serves as the reference, and in addition, it will show up in the display at runtime.

| -------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Parameter      | Example         | Description                                                                                                                     |

  
  
---

[variables]

Variables can be defined in the configuration file using the $varname=value syntax. Variables defined on the command line (-w varname=value) take precedence and do not create conflicts with variables defined in the configuration file. Variables are used in the configuration file using the $varname syntax: each instance of $varname is replaced by its associated value. This is typically useful if the same parameter must be used at several places. For instance, you might want to have multiple load balancers, all transmitting to the same set of worker cores. The list of worker cores could then be defined once in a variable:

[variables]
$wk=1s0-5s0

Then, a load balancer definition would use the variable:

[core 6s0]
name=LB
task=0
mode=lbnetwork
tx cores=$wk task=0
...

And the section defining the worker cores would be:

[core $wk]
name=worker
task=0
mode=qinqencapv4
...

---
  

  
