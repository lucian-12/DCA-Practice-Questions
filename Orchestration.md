Answers Orchestration
=====================

**Answer 1: b**

#### Explanation

While **placement constraints** limit the nodes a service can run
on, **placement preferences** try to place tasks on appropriate nodes in
an algorithmic way (currently, only spread evenly).

For instance, if you assign each node a rack label, you can set a
placement preference to spread the service evenly across nodes with the
rack label, by value.

[Placement
constraints](https://docs.docker.com/engine/swarm/services/#placement-constraints) let
you configure the service to run only on nodes with specific (arbitrary)
metadata set, and cause the deployment to fail if appropriate nodes do
not exist.

<https://docs.docker.com/engine/swarm/services/#control-service-placement>

**Answer 2: c**

#### Explanation

**Distribute manager nodes**

In addition to maintaining an odd number of manager nodes, pay attention
to datacenter topology when placing managers.

For optimal fault-tolerance, distribute manager nodes across a minimum
of 3 availability-zones to support failures of an entire set of machines
or common maintenance scenarios.

If you suffer a failure in any of those zones, the swarm
should **maintain the quorum** of manager nodes available to process
requests and rebalance workloads.

Swarm manager nodes         Repartition (on 3 Availability zones)

3                                              1-1-1

5                                              2-2-1

7                                              3-2-2

9                                              3-3-3

<https://docs.docker.com/engine/swarm/admin_guide/#distribute-manager-nodes>
