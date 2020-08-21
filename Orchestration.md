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

#### **Answer 8: c**

Explanation:

To set the maximum amount of memory the container can use one of the
following flags

-m or \--memory= or \--memory

Possible values can take a positive integer, followed by a suffix of b,
k, m, g to indicate bytes, kilobytes, megabytes, or gigabytes.

<https://docs.docker.com/config/containers/resource_constraints/#memory>

#### **Answer 9: a, d**

Explanation:

To scale one or multiple replicated services use:

docker service scale SERVICE=REPLICAS \[SERVICE=REPLICAS\...\]

The following command scales the "web" service to 5 tasks.

docker service scale web=5

Alternatively, you can use:

docker service update \--replicas

For example

docker service update \--replicas=5 web

This example also updates the number of replicas for the service to 5.

<https://docs.docker.com/engine/reference/commandline/service_scale/>

<https://docs.docker.com/engine/reference/commandline/service_update/>

#### **Answer 10: c**

Explanation:

To display detailed information on one or more containers including the
list of volume use:

docker container inspect \[OPTIONS\] CONTAINER \[CONTAINER\...\]

<https://docs.docker.com/engine/reference/commandline/container_inspect/>

#### **Answer 11: a**

Explanation:

To update a service use:

docker service update \[OPTIONS\] SERVICE

<https://docs.docker.com/engine/reference/commandline/service_update/>

#### **Answer 12: a**

Explanation:

**Tasks and scheduling**

A **task** is the atomic unit of scheduling within a swarm. When you
declare a desired service state by creating or updating a service, the
orchestrator realizes the desired state by scheduling tasks.

For instance, you define a service that instructs the orchestrator to
keep three instances of an HTTP listener running at all times. The
orchestrator responds by creating three tasks. Each task is a slot that
the **scheduler** fills by spawning a container.

<https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/#tasks-and-scheduling>

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/tasks_and_scheduling.jpg)

#### **Answer 13: a**

Explanation:

The scale command enables you to scale one or more **replicated
services** either up or down to the desired number of replicas.

This command cannot be applied to services which
are **global** **services**.

The following command tries to scale a global service to 10 tasks and
returns an error.

\$ docker service create \--mode global \--name backend backend:latest

b4g08uwuairexjub6ome6usqh

\$ docker service scale backend=10

backend: scale can only be used with replicated mode

<https://docs.docker.com/engine/reference/commandline/service_scale/>

#### **Answer 14: a**

Explanation:

The following command shows all the tasks that are part of the redis
service:

\$ docker service ps redis

In addition to running tasks, the output also shows the task history.
For example, after updating the service to use the redis:3.0.6 image,
the output may look like this:

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageHistory.png)

The number of items in the task history is determined by the
\--task-history-limit option that was set when initializing the swarm.

<https://docs.docker.com/engine/reference/commandline/service_ps/>

#### **Answer 15: a**

Explanation:

**Tasks and scheduling**

A task is the atomic unit of scheduling within a swarm. When you declare
a desired service state by creating or updating a service via HTTP API
endpoints, the **orchestrator** realizes the desired state by scheduling
tasks.

For instance, you define a service that instructs
the **orchestrator** to keep three instances of an HTTP listener running
at all times. The **orchestrator** **responds** by creating three tasks.
Each task is a slot that the scheduler fills by spawning a container.

<https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/#tasks-and-scheduling>

### **Answer 16: c, d**

Explanation:

To display detailed information on one or more containers, use:

docker container inspect \[OPTIONS\] CONTAINER \[CONTAINER\...\]

<https://docs.docker.com/engine/reference/commandline/container_inspect/>

### **Answer 17: a**

Explanation:

By default, ports are published using **ingress mode**.

This means that the swarm routing mesh makes the service accessible at
the published port on every node regardless if there is a task for the
service running on the node.

However, if you set **host mode **explicitly, the port is only bound on
nodes where the service is running, and a given port on a node can only
be bound once. You can only set the publication mode using the long
syntax.

You can publish service ports to make them available externally to the
swarm using the \--publish flag.

The \--publish flag can take two different styles of arguments.

The short version is positional and allows you to specify the published
port and target port separated by a colon (:).

\$ docker service create \--name my_web \--replicas 3 \--publish 8080:80
nginx

Here, the published port is 8080 and the target port is of the container
is 80.

There is also a long format, which is easier to read and allows you to
specify more options.

\$ docker service create \--name my_web \--replicas 3 \--publish
published=8080,target=80 nginx

<https://docs.docker.com/engine/reference/commandline/service_create/#publish-service-ports-externally-to-the-swarm--p---publish>

### **Answer 18: c**

Explanation:

While **placement constraints** limit the nodes a service can run
on, **placement preferences** try to place tasks on appropriate nodes in
an algorithmic way (currently, only spread evenly). For instance, if you
assign each node a rack label, you can set a placement preference to
spread the service evenly across nodes with the rack label, by value.
This way, if you lose a rack, the service is still running on nodes on
other racks.

Placement preferences are not strictly enforced. If no node has the
label you specify in your preference, the service is deployed as though
the preference was not set.

The following example sets a preference to spread the deployment across
nodes based on the value of the datacenter label. If some nodes have
datacenter=us-east and others have datacenter=us-west, the service is
deployed as evenly as possible across the two sets of nodes.

\$ docker service create \\

\--replicas 9 \\

\--name redis_2 \\

\--placement-pref \'spread=node.labels.datacenter\' \\

redis:3.0.6

When updating a service with docker service update,
\--placement-pref-add appends a new placement preference after all
existing placement preferences. \--placement-pref-rm removes an existing
placement preference that matches the argument.

In this diagram the containers are first placed by datacenters and then
by the rack.

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/placement.png)

<https://docs.docker.com/engine/swarm/services/#control-service-placement>
