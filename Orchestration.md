Answers Orchestration
=====================

#### **Answer 1: b**

Explanation:

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

#### **Answer 2: c**

Explanation:

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

#### **Answer 3: a**

Explanation:

A Pod (as in a pod of whales or pea pod) is a group of one or more
containers (such as Docker containers), with shared storage/network, and
a specification for how to run the containers.

A Pod\'s contents are always co-located and co-scheduled, and run in a
shared context. A Pod models an application-specific \"logical host\" -
it contains one or more application containers which are relatively
tightly coupled --- in a pre-container world, being executed on the same
physical or virtual machine would mean being executed on the same
logical host.

<https://kubernetes.io/docs/concepts/workloads/pods/pod/#what-is-a-pod>

#### **Answer 4: b**

Explanation:

**Formatting**

The formatting option \--format pretty-prints container output using a
Go template.

When using the \--format option, the ps command will either output the
data exactly as the template declares or, when using the table
directive, includes column headers as well.

<https://docs.docker.com/engine/reference/commandline/ps/#formatting>

The following example uses a template without headers and outputs the
ID, name and status entries separated by a colon (:) for all running
containers.

Use "\\t" for extra space between columns.

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/outputDockerps.png)

#### **Answer 5: b**

Explanation:

In a swarm of N managers, a quorum (a majority) of manager nodes must
always be available. For example, in a swarm with five managers, a
minimum of three must be operational and in communication with each
other. In other words, the swarm can tolerate up
to **(N-1)/2** permanent failures beyond which requests involving swarm
management cannot be processed.

An odd number of managers is recommended because the next even number
does not make the quorum easier to keep. For instance, whether you have
3 or 4 managers, you can still only lose 1 manager and maintain the
quorum. If you have 5 or 6 managers, you can still only lose two.

<https://docs.docker.com/engine/swarm/admin_guide/#maintain-the-quorum-of-managers>

#### **Answer 6: c**

Explanation:

To **deploy** your application to a swarm, you **submit a service
definition** to a manager node. The manager node **dispatches** units of
work called **tasks** to worker **nodes**.

<https://docs.docker.com/engine/swarm/key-concepts/#nodes>

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/tasks_and_scheduling.jpg)

#### **Answer 7: c**

Explanation:

REPLICATED OR GLOBAL SERVICES

Swarm mode has two types of services: replicated and global. For
replicated services, you specify the number of replica tasks for the
swarm manager to schedule onto available nodes. For global services, the
scheduler places one task on each available node that meets the
service's placement constraints and resource requirements.

You control the type of service using the \--mode flag. If you don't
specify a mode, the service defaults to replicated.

<https://docs.docker.com/engine/swarm/services/#replicated-or-global-services>

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/globalVsreplicated.jpg)
