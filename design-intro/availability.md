## Availability (AKA Fault Tolerance)

How resistant a system is to failure

Measuring availability

- Nines
  - 99% - two nines of availability
  - 99.5% two and a half nines
  - 99.9% - three nines of availability
  - 99.999% - 5.25 minutes of downtime per year

SLA/SLO

### Service Level Agreement

- A collection of guarantees given to a customer by a service provider. SLAs typically make guarantees on a system's availability, amonst other things. SLAs are made up of one or multiple SLOs.

### Service Level Objective

A guarantee given to a customer by a service provider. SLOs typically make guarantees on a system's availability, amonst other things. SLOs constitute an SLA.

### Redundancy

- The act of duplicating or triplicating certain parts of a system
- When adding redundant servers, use a load balancer
  - What if the load balancer becomes overloaded?
    - add redundancy in load balancers
- Passive Redundancy - a jet has two engines, if an engine fails, the plane can still land safely
- Active Redundancy - having multiple machines that work together when only one or few machines are doing most of the work and eventually fails, the idle machines will then take over the work
