About Application Security Groups
--------------------------------------

Application Security Groups (ASGs) are a collections of egress rules that 
specify the protocols, ports, and IP address ranges where app or task 
instances send traffic.

ASGs define allow rules, and their order of evaluation is unimportant when
multiple ASGs apply to the same space or deployment. 

The platform sets up rules to filter and log outbound network traffic 
from app and task instances. 

ASGs apply to both buildpack-based and Docker-based apps and tasks.


Staging and Running ASGs
------------------------------

Administrators can define a staging ASG for app and task staging, and a 
running ASG for app and task runtime.

When apps or tasks begin staging, they require traffic rules permissive 
enough to allow them to pull resources from the network. 

A running app or task no longer needs to pull resources, so traffic rules 
can be more restrictive and secure. 

To distinguish between these two security requirements, administrators can 
define a staging ASG for app and task staging with more permissive rules,
and a running ASG for app and task runtime with less permissive rules.