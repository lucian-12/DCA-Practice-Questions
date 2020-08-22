Answers Orchestration
=====================

### **Answer 1: b**

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

### **Answer 2: c**

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

### **Answer 3: a**

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

### **Answer 4: b**

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

### **Answer 5: b**

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

### **Answer 6: c**

Explanation:

To **deploy** your application to a swarm, you **submit a service
definition** to a manager node. The manager node **dispatches** units of
work called **tasks** to worker **nodes**.

<https://docs.docker.com/engine/swarm/key-concepts/#nodes>

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/tasks_and_scheduling.jpg)

### **Answer 7: c**

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

### **Answer 8: c**

Explanation:

To set the maximum amount of memory the container can use one of the
following flags

    -m or --memory= or --memory

Possible values can take a positive integer, followed by a suffix of b,
k, m, g to indicate bytes, kilobytes, megabytes, or gigabytes.

<https://docs.docker.com/config/containers/resource_constraints/#memory>

### **Answer 9: a, d**

Explanation:

To scale one or multiple replicated services use:

    docker service scale SERVICE=REPLICAS [SERVICE=REPLICAS...]

The following command scales the "web" service to 5 tasks.

    docker service scale web=5

Alternatively, you can use:

    docker service update --replicas

For example

    docker service update --replicas=5 web

This example also updates the number of replicas for the service to 5.

<https://docs.docker.com/engine/reference/commandline/service_scale/>

<https://docs.docker.com/engine/reference/commandline/service_update/>

### **Answer 10: c**

Explanation:

To display detailed information on one or more containers including the
list of volume use:

    docker container inspect [OPTIONS] CONTAINER [CONTAINER...]

<https://docs.docker.com/engine/reference/commandline/container_inspect/>

### **Answer 11: a**

Explanation:

To update a service use:

    docker service update [OPTIONS] SERVICE

<https://docs.docker.com/engine/reference/commandline/service_update/>

### **Answer 12: a**

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

### **Answer 13: a**

Explanation:

The scale command enables you to scale one or more **replicated
services** either up or down to the desired number of replicas.

This command cannot be applied to services which
are **global** **services**.

The following command tries to scale a global service to 10 tasks and
returns an error.

    $ docker service create --mode global --name backend backend:latest

    b4g08uwuairexjub6ome6usqh

    $ docker service scale backend=10

    backend: scale can only be used with replicated mode

<https://docs.docker.com/engine/reference/commandline/service_scale/>

### **Answer 14: a**

Explanation:

The following command shows all the tasks that are part of the redis
service:

    $ docker service ps redis

In addition to running tasks, the output also shows the task history.
For example, after updating the service to use the redis:3.0.6 image,
the output may look like this:

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageHistory.png)

The number of items in the task history is determined by the
\--task-history-limit option that was set when initializing the swarm.

<https://docs.docker.com/engine/reference/commandline/service_ps/>

### **Answer 15: a**

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

    docker container inspect [OPTIONS] CONTAINER [CONTAINER...]

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

    $ docker service create --name my_web --replicas 3 --publish 8080:80
    nginx

Here, the published port is 8080 and the target port is of the container
is 80.

There is also a long format, which is easier to read and allows you to
specify more options.

    $ docker service create --name my_web --replicas 3 --publish
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

    $ docker service create \

    --replicas 9 \

    --name redis_2 \

    --placement-pref 'spread=node.labels.datacenter' \

    redis:3.0.6

When updating a service with docker service update,
\--placement-pref-add appends a new placement preference after all
existing placement preferences. \--placement-pref-rm removes an existing
placement preference that matches the argument.

In this diagram the containers are first placed by datacenters and then
by the rack.

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/placement.png)

<https://docs.docker.com/engine/swarm/services/#control-service-placement>

### **Answer 19: d**

Explanation:

You can print the inspect output in a human-readable format instead of
the default JSON output, by using the \--pretty option.

https://docs.docker.com/engine/reference/commandline/service_inspect/\#formatting

### **Answer 20: a**

Explanation:

Since the service its newly create we use

    docker service create [OPTIONS] IMAGE [COMMAND] [ARG...]

Use the \--replicas flag to set the number of replica tasks for a
replicated service.

The following command creates a redis service with 5 replica tasks:

    $ docker service create --name redis --replicas=5 redis:3.0.6

<https://docs.docker.com/engine/reference/commandline/service_create/#create-a-service-with-5-replica-tasks---replicas>

### **Answer 21: c**

Explanation:

Docker inspect provides detailed information on constructs controlled by
Docker.

By default, docker inspect will render results in a JSON array.

<https://docs.docker.com/engine/reference/commandline/inspect/>

### **Answer 22: c**

Explanation:

To remove a node from the swarm use the following on the node itself:

    docker swarm leave [OPTIONS]

When you run this command on a worker, that worker leaves the swarm.

You can use the \--force option on a manager to remove it from the
swarm. However, this does not reconfigure the swarm to ensure that there
are enough managers to maintain a quorum in the swarm.

The safe way to remove a manager from a swarm is to demote it to a
worker and then direct it to leave the quorum without using \--force.

<https://docs.docker.com/engine/reference/commandline/swarm_leave/>

### **Answer 23: a, c, d**

Explanation:

Required Fields

In the .yaml file for the Kubernetes object you want to create, you\'ll
need to set values for the following fields:

apiVersion - Which version of the Kubernetes API you\'re using to create
this object

kind - What kind of object you want to create

metadata - Data that helps uniquely identify the object, including a
name string, UID, and an optional namespace

spec - What state you desire for the object

<https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/#required-fields>

### **Answer 24: a, b, c**

Explanation:

If you\'d like to **start sending traffic** to a Pod only when a probe
succeeds, specify a readiness probe. In this case, the readiness probe
might be the same as the liveness probe, but the existence of the
readiness probe in the spec means that the Pod will start without
receiving any traffic and only start receiving traffic after the probe
starts succeeding. If your Container needs to work on **loading large
data, configuration files, or migrations during startup**, specify a
readiness probe.

If you want your Container to be able to take itself **down for
maintenance**, you can specify a readiness probe that checks an endpoint
specific to readiness that is different from the liveness probe.

Note that if you just want to be able to drain requests when the Pod is
deleted, you do not necessarily need a readiness probe; on deletion, the
Pod automatically puts itself into an unready state regardless of
whether the readiness probe exists. The Pod remains in the unready state
while it waits for the Containers in the Pod to stop.

<https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#when-should-you-use-a-readiness-probe>

### **Answer 25: b**

Explanation:

To return low-level information on Docker objects use:

    docker inspect [OPTIONS] NAME|ID [NAME|ID...]

<https://docs.docker.com/engine/reference/commandline/inspect/>

### **Answer 26: b**

Explanation:

To configure the restart policy for a container, use the \--restart flag
when using the docker run command. The value of the \--restart flag can
be any of the following:

· **no** - Do not automatically restart the container. (the default)

· **on-failure** - Restart the container if it exits due to an error,
which manifests as a non-zero exit code.

· **always** - Always restart the container if it stops. If it is
manually stopped, it is restarted only when Docker daemon restarts or
the container itself is manually restarted. (See the second bullet
listed in restart policy details)

· **unless-stopped** - Similar to always, except that when the container
is stopped (manually or otherwise), it is not restarted even after
Docker daemon restarts.

<https://docs.docker.com/config/containers/start-containers-automatically/>

### **Answer 27: b**

Explanation:

A task is a one-directional mechanism.

This means that it progresses monotonically through a series of states:
assigned, prepared, running, etc. If the task fails the orchestrator
removes the task and its container and then creates a new task to
replace it according to the desired state specified by the service.

<https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/#tasks-and-scheduling>

### **Answer 28: d**

Explanation:

    docker inspect command returns low-level information on Docker objects.

<https://docs.docker.com/engine/reference/commandline/inspect/>

### **Answer 29: b**

Explanation:

**Publish service ports externally to the swarm (-p, \--publish)**

You can publish service ports to make them available externally to the
swarm using the \--publish flag.

The \--publish flag can take two different styles of arguments. The
short version is positional, and allows you to specify the published
port and target port separated by a colon (:).

    $ docker service create --name my_web --replicas 3 --publish 8080:80
    nginx

There is also a long format, which is easier to read and allows you to
specify more options. The long format is preferred. You cannot specify
the service's mode when using the short format.

Here is an example of using the long format for the same service as
above:

    $ docker service create --name my_web --replicas 3 --publish
    published=8080,target=80 nginx

You can also specify the protocol to use, tcp, udp, or sctp. Defaults to
tcp. To bind a port for both protocols, specify the -p or \--publish
flag twice.

    $ docker service create --name my_web --replicas 3 --publish
    8080:80/udp nginx

<https://docs.docker.com/engine/reference/commandline/service_create/#publish-service-ports-externally-to-the-swarm--p---publish>

### **Answer 30: d**

Explanation:

You can change almost everything about an existing service using
the docker service update command.

When creating a service, use the -p or \--publish flag.

When updating an existing service, use the flag is \--publish-add. There
is also a \--publish-rm flag to remove a port that was previously
published.

<https://docs.docker.com/engine/reference/commandline/service_update/#add-or-remove-published-service-ports>

### **Answer 31: d**

Explanation:

Docker manager nodes store the swarm state and manager logs in
the **/var/lib/docker/swarm/** directory.

Usually, on Linux distributions:

\"/**etc**\" is used for configurations (.conf files etc). here you find
all the configs and settings for your system.

\"/**var**\" is usually used for log files, \'temporary\' files (like
mail spool, printer spool, etc), databases, and all other data not tied
to a specific user. Logs are usually in \"/var/log\", databases in
\"/var/lib\" (mysql - \"/var/lib/mysql\"), etc.

<https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard>

### **Answer 32: d**

Explanation:

To deploy an application image when Docker Engine is in swarm mode, you
create a service. Frequently a service is the image for a microservice
within the context of some larger application.

Examples of services might include an HTTP server, a database, or any
other type of executable program that you wish to run in
a **distributed** environment.

<https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/>

#### Answer 33: d

Explanation:

**Tasks and scheduling**

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/tasks_and_scheduling.jpg)

#### Answer 34: b, c

Explanation:

Using either docker-compose.yml or a stack.

If the service is replicated (which is the default), specify the number
of containers that should be running at any given time in the yml file.

<https://docs.docker.com/compose/compose-file/>

    version: "3.8"

    services:

    worker:

        image: dockersamples/worker

        deploy:

          mode: replicated

          replicas: 6

#### Answer 35: c

Explanation:

To set environment variables use -e or --env flags:

For example, this sets an environment variable for all tasks in a
service:

    $ docker service create \

      --name redis_2 \

      --replicas 5 \

      --env MYVAR=foo \

      redis:3.0.6

Alternatively, you can use **templates** for some flags of service
create, using the syntax provided by the Go's text/template package.

The supported flags are the following :

\--hostname

\--mount

\--env

Valid placeholders for the Go template are listed below:

**Placeholder                Description**

.Service.ID                  Service ID

.Service.Name           Service name

.Service.Labels          Service labels

.Node.ID                     Node ID

.Node.Hostname       Node Hostname

.Task.ID                       Task ID

.Task.Name                 Task name

.Task.Slot                    Task slot

For example, we are going to set the template of the created containers
based on the service's name, the node's ID, and the hostname where it
sits.

    $ docker service create \

        --name hosttempl \

        --env="{{.Node.ID}}"\

        --hostname="{{.Node.Hostname}}-{{.Service.Name}}"\

        busybox top

<https://docs.docker.com/engine/reference/commandline/service_create/#create-services-using-templates>

#### Answer 36: c

Explanation:

You control the type of service using the \--mode flag.

If you don't specify a mode, the service defaults to replicated.

For replicated services, you specify the number of replica tasks you
want to start using the \--replicas flag. For example, to start a
replicated nginx service with 3 replica tasks:

    $ docker service create \

    --name my_web \

    --replicas 3 \

    nginx

To start a global service on each available node, pass \--mode global to
docker service create. Every time a new node becomes available, the
scheduler places a task for the global service on the new node. For
example to start a service that runs alpine on every node in the swarm:

    $ docker service create \

    --name myservice \

    --mode global \

    alpine top

<https://docs.docker.com/engine/swarm/services/#replicated-or-global-services>

#### Answer 37: d

Explanation:

Sometimes, such as planned maintenance times, you need to set a node to
DRAIN availability.

DRAIN availability prevents a node from receiving new tasks from the
swarm manager.

It also means the manager stops tasks running on the node and launches
replica tasks on a node with ACTIVE availability.

<https://docs.docker.com/engine/swarm/swarm-tutorial/drain-node/>

#### Answer 38: b

Explanation:

The following flags are supported by docker service create command:

    --label , -l

Service labels in order to set metadata on a service.

    --publish , -p

Publish a port as a node port

    --tty , -t

Allocate a pseudo-TTY

**docker service** command does not support -v or --volume flags.
Instead the \--mount flag is used when creating the service, or
\--mount-add when updating the service.

The type of mount can be either volume, bind, tmpfs, or npipe. Defaults
to **volume** if no type is specified.

For example:

    $ docker service create \

    --name my-service \

    --replicas 3 \

    --mount type=volume,source=my-volume,destination=/path/in/container \

    nginx:alpine

Here, for each replica of the service, the engine requests a volume
named "my-volume" from the default ("local") volume driver where the
task is deployed. If the volume does not exist, the engine creates a new
volume.

<https://docs.docker.com/engine/reference/commandline/service_create/#add-bind-mounts-volumes-or-memory-filesystems>

#### Answer 39: d

Explanation:

To update metadata about a node, such as its availability, labels, or
roles use:

    docker node update [OPTIONS] NODE

To add or update a node label (key=value) use:

    docker node update --label-add NODE

<https://docs.docker.com/engine/reference/commandline/node_update/>

#### Answer 40: d

Explanation:

Here are a few examples of when a service might remain in state pending.

· If all nodes are paused or drained, and you create a service, it is
pending until a node becomes available. In reality, the first node to
become available gets all of the tasks, so this is not a good thing to
do in a production environment.

· You can reserve a specific amount of memory for a service. If no node
in the swarm has the required amount of memory, the service remains in a
pending state until a node is available which can run its tasks. If you
specify a very large value, such as 500 GB, the task stays pending
forever, unless you really have a node which can satisfy it.

· You can impose placement constraints on the service, and the
constraints may not be able to be honored at a given time.

<https://docs.docker.com/engine/swarm/how-swarm-mode-works/services/#pending-services>

#### Answer 41: d

Explanation:

When you create a service, you define its optimal state, that is, a
number
of **replicas**, **network** and **storage** **resources** available to
it, ports the service exposed to the outside world, and more).

<https://docs.docker.com/engine/swarm/key-concepts/#what-is-a-swarm>

    --secret Specify secrets to expose to the service

    --network Network attachments

    --mount Attach a filesystem mount to the service

DIFFERENCES BETWEEN "\--MOUNT" AND "\--VOLUME"

The \--mount flag supports most options that are supported by the -v or
\--volume flag for docker run, with some important exceptions:

Here all available configuration options when creating a service.

<https://docs.docker.com/engine/reference/commandline/service_create/>

#### Answer 42: c

Explanation:

**Choosing your orchestrator**

Docker Enterprise provides access to the full API sets of three popular
orchestrators:

· **Kubernetes**: full YAML object support

· **SwarmKit**: Service-centric, Compose file version 3

· "**Classic" Swarm**: Container-centric, Compose file version 2

Docker Enterprise proxies the underlying API of each orchestrator,
giving you access to all of the capabilities of each orchestrator, along
with the benefits of Docker Enterprise, like role-based access control
and Docker Content Trust.

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/dockerEEAPI.jpg)

#### Answer 43: c

Explanation:

There are different kinds of resources for creating Pods:

· Use a Deployment, ReplicaSet or StatefulSet for Pods that are not
expected to terminate, for example, web servers.

· Use a Job for Pods that are expected to terminate once their work is
complete; for example, batch computations. Jobs are appropriate only for
Pods with restartPolicy equal to OnFailure or Never.

· Use a DaemonSet for Pods that need to run one per eligible node.

<https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-lifetime>

#### Answer 44: d

Explanation:

REPLICATED OR GLOBAL SERVICES

Swarm mode has two types of services: replicated and global.

For replicated services, you specify the number of replica tasks for the
swarm manager to schedule onto available nodes.

For global services, the scheduler places one task on each available
node that meets the service's placement constraints and resource
requirements.

<https://docs.docker.com/engine/swarm/services/#replicated-or-global-services>

#### Answer 45: b, c, d

Explanation:

You can define one or multiple topologySpreadConstraint to instruct the
kube-scheduler on how to place each incoming Pod in relation to the
existing Pods across your cluster. The fields are:

· **maxSkew** describes the degree to which Pods may be unevenly
distributed. It\'s the maximum permitted difference between the number
of matching Pods in any two topology domains of a given topology type.
It must be greater than zero.

· **topologyKey** is the key of node labels. If two Nodes are labelled
with this key and have identical values for that label, the scheduler
treats both Nodes as being in the same topology. The scheduler tries to
place a balanced number of Pods into each topology domain.

· **whenUnsatisfiable** indicates how to deal with a Pod if it doesn\'t
satisfy the spread constraint: DoNotSchedule (default) tells the
scheduler not to schedule it. ScheduleAnyway tells the scheduler to
still schedule it while prioritizing nodes that minimize the skew.

· **labelSelector** is used to find matching Pods. Pods that match this
label selector are counted to determine the number of Pods in their
corresponding topology domain. See Label Selectors for more details.

<https://kubernetes.io/docs/concepts/workloads/pods/pod-topology-spread-constraints/#spread-constraints-for-pods>

#### Answer 46: a

Explanation:

Memory reservation is a kind of memory soft limit that allows for
greater sharing of memory. Under normal circumstances, containers can
use as much of the memory as needed and are constrained only by the hard
limits set with the -m/\--memory option.

When memory reservation is set, Docker detects memory contention or low
memory and forces containers to restrict their consumption to a
reservation limit.

To set the maximum amount of memory the container can use one of the
following.

-m or \--memory=

To specify a soft limit which is activated when Docker detects
contention or low memory on the host machine use the following
flag:\--memory-reservation

If you use \--memory-reservation, it must be set lower than \--memory
for it to take precedence. Because it is a soft limit, it does not
guarantee that the container doesn't exceed the limit.

<https://docs.docker.com/config/containers/resource_constraints/#memory>

<https://docs.docker.com/engine/reference/run/#user-memory-constraints>

#### Answer 47: d

Explanation:

You can change almost everything about an existing service using
the docker service update command.

When creating a service, use the -p or \--publish flag.

When updating an existing service, use the flag is \--publish-add. There
is also a \--publish-rm flag to remove a port that was previously
published.

Assuming that the my_web service exists, use the following command to
remove the published port 80.

    $ docker service update --publish-rm 80 my_web

<https://docs.docker.com/engine/swarm/services/#update-a-service>

#### Answer 48: d

Explanation:

You can change node availability.

For example, to change a manager node to Drain availability use:

    $ docker node update --availability drain node-1

<https://docs.docker.com/engine/swarm/manage-nodes/#change-node-availability>

This is useful when you want to:

· drain a manager node so that only performs swarm management tasks and
is unavailable for task assignment.

· drain a node so you can take it down for maintenance.

<https://docs.docker.com/engine/swarm/swarm-tutorial/drain-node/>

#### Answer 49: a

Explanation:

Setting a node to DRAIN does not remove standalone containers from that
node, such as those created with docker run, docker-compose up, or the
Docker Engine API.

A node's status, including DRAIN, only affects the node's ability to
schedule swarm service workloads.

<https://docs.docker.com/engine/swarm/swarm-tutorial/drain-node/>

DRAIN availability prevents a node from receiving new tasks from the
swarm manager. It also means the manager stops tasks running on the node
and launches replica tasks on a node with ACTIVE availability.

<https://docs.docker.com/engine/swarm/swarm-tutorial/drain-node/>

#### Answer 50: b

Explanation:

Containers running in a service are called "tasks" or "replicas".

To scale the number of containers in the service you can use one of the
following commands.

    $ docker service scale <SERVICE-ID>=<NUMBER-OF-TASKS>

    $ docker service update --replicas=<NUMBER-OF-TASKS> <SERVICE-ID>

For example, these commands are equivalent:

    $ docker service scale web=5

    $ docker service update --replicas=5 web

<https://docs.docker.com/engine/swarm/swarm-tutorial/scale-service/>

#### Answer 51: b

Explanation:

A **node** is an instance of the Docker engine participating in the
swarm. You can also think of this as a Docker node.

You can run one or more nodes on a single physical computer or cloud
server, but production swarm deployments typically include Docker nodes
distributed across multiple physical and cloud machines.

<https://docs.docker.com/engine/swarm/key-concepts/#nodes>

#### Answer 52: b

Explanation:

To rollback a specified service to its previous version from the swarm
you can execute one of the following commands:

    docker service rollback [OPTIONS] SERVICE

    docker service update --rollback SERVICE

<https://docs.docker.com/engine/reference/commandline/service_rollback/>

#### Answer 53: c

Explanation:

When using \'docker service create\' and \'docker service update\' you
can set a \--update-delayflag to delay between updates.

For example:

    $ docker service update --update-delay 30s redis

The \--update-delay 30s setting introduces a 30 second delay between
tasks so that the rolling restart happens gradually.

You can use the following units ns\|us\|ms\|s\|m\|h.

<https://docs.docker.com/engine/reference/commandline/service_update/#perform-a-rolling-restart-with-no-parameter-changes>

#### Answer 54: a, b, d

Explanation:

A Secret is an object that contains a small amount of sensitive data
such as a password, a token, or a key. Such information might otherwise
be put in a Pod specification or in an image. Users can create secrets
and the system also creates some secrets.

To use a secret, a Pod needs to reference the secret. A secret can be
used with a Pod in three ways:

· As files in a volume mounted on one or more of its containers.

· As container environment variable.

· By the kubelet when pulling images for the Pod.

<https://kubernetes.io/docs/concepts/configuration/secret/#overview-of-secrets>

#### Answer 55: b

Explanation:

To remove a node from the swarm use the following on the node itself:

    docker swarm leave [OPTIONS]

When you run this command on a worker itself, that worker leaves the
swarm.

<https://docs.docker.com/engine/reference/commandline/swarm_leave/>

#### Answer 56: a

Explanation:

To configure the restart policy for a container, use the \--restart flag
when using the docker run command. The value of the \--restart flag can
be any of the following:

· **no** - Do not automatically restart the container. (the default)

· **on-failure** - Restart the container if it exits due to an error,
which manifests as a non-zero exit code.

· **always** - Always restart the container if it stops. If it is
manually stopped, it is restarted only when Docker daemon restarts or
the container itself is manually restarted. (See the second bullet
listed in restart policy details)

· **unless-stopped** - Similar to always, except that when the container
is stopped (manually or otherwise), it is not restarted even after
Docker daemon restarts.

<https://docs.docker.com/config/containers/start-containers-automatically/>

#### Answer 57: d

Explanation:

To list the tasks that are running as part of the specified services
use:

    docker service ps [OPTIONS] SERVICE [SERVICE...]

<https://docs.docker.com/engine/reference/commandline/service_ps/>

#### Answer 58: b

Explanation:

Containers can join multiple networks that allow you to provide
fine-grained network policy for connectivity and isolation.

By default, a container will be created with one network attached. If no
network is specified then this will be the default docker0 network.

After the container has been created more networks can be attached to a
container using the docker network connect command.

Docker only **allows a single network** to be specified with the docker
run command. To connect multiple networks docker network connect is used
to connect additional networks.

https://success.docker.com/article/multiple-docker-networks

#### Answer 59: a

Explanation:

By default, swarm services can run on any node in the cluster. If you
choose to constrain where services run, please note the following
examples.

To ensure a service runs on worker nodes rather than managers, use
a **node.role** constraint in the service definition. For example:

    docker service create \

        --name nginx-workers-only \

        --constraint node.role==worker \

        nginx

<https://success.docker.com/article/using-contraints-and-labels-to-control-the-placement-of-containers>

Constraint expressions can either use a match (==) or exclude (!=) rule.
Multiple constraints find nodes that satisfy every expression (AND
match).

<https://docs.docker.com/engine/reference/commandline/service_create/#specify-service-constraints---constraint>

#### Answer 60: d

Explanation:

Tasks advance through a number of states until they complete or fail.

Tasks are initialized in the NEW state.

The task progresses forward through a number of states, and its state
doesn't go backward. For example, a task never goes from COMPLETE to
RUNNING.

<https://docs.docker.com/engine/swarm/how-swarm-mode-works/swarm-task-states/>

#### Answer 61: a, b

Explanation:

**Maintain the quorum of managers**

If the swarm loses the quorum of managers, the swarm **cannot perform
administrative tasks** such as scaling or updating services and joining
or removing nodes from the swarm.

Nevertheless, tasks on existing worker nodes continue to run.

Swarm is resilient to failures and the swarm can recover from any number
of temporary node failures (machine reboots or crash with restart) or
other transient errors. However, a swarm cannot automatically recover if
it loses a quorum.

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

#### Answer 62: a

Explanation:

REPLICATED OR GLOBAL SERVICES

Swarm mode has two types of services: replicated and global.

For replicated services, you specify the number of replica tasks for the
swarm manager to schedule onto available nodes.

For global services, the scheduler places one task on each available
node that meets the service's placement constraints and resource
requirements.

<https://docs.docker.com/engine/swarm/services/#replicated-or-global-services>

#### Answer 63: c

Explanation:

When you start a service and define a volume, each service container
uses its own local volume. None of the containers can share this data if
you use the local volume driver, but some volume drivers do support
shared storage.

The following example starts a nginx service with four replicas, each of
which uses a local volume called myvol2.

    $ docker service create -d \

    --replicas=4 \

    --name devtest-service \

    --mount source=myvol2,target=/app \

    nginx:latest

<https://docs.docker.com/storage/volumes/#start-a-service-with-volumes>

To update a service to add or update a mount on a service use:

    $ docker service update --mount-add SERVICE

<https://docs.docker.com/engine/reference/commandline/service_update/>

#### Answer 64: c

Explanation:

To prevent the scheduler from placing tasks on a manager node in a
multi-node swarm, set the availability for the manager node
to **Drain**.

The scheduler gracefully stops tasks on nodes in Drain mode and
schedules the tasks on an Active node. The scheduler does not assign new
tasks to nodes with Drain **availability**.

<https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/#worker-nodes>

You can change node availability.

For example, to change a manager node to Drain availability use:

    $ docker node update --availability drain node-1

This is useful when you want to:

· drain a manager node so that only performs swarm management tasks and
is unavailable for task assignment.

· drain a node so you can take it down for maintenance.

<https://docs.docker.com/engine/swarm/manage-nodes/#change-node-availability>

#### Answer 65: d

Explanation:

Swarm never creates individual containers. Instead, all Swarm workloads
are scheduled as services, which are scalable groups of containers. Each
of the services has a certain number of replicas or tasks.

A **stack** is used to describe a collection of swarm services that are
related, most probably because they are part of the same application.

In that sense, we could also say that a stack describes an application
that consists of one to many services that we want to run on the swarm.

<https://docs.docker.com/get-started/swarm-deploy/#describe-apps-using-stack-files>

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/stack.jpg)

#### Answer 66: d

Explanation:

The command to initialize a swarm is:

    docker swarm init [OPTIONS]

<https://docs.docker.com/engine/reference/commandline/swarm_init/>

When you run the docker swarm init command to create a swarm, the Docker
Engine starts running in swarm mode and it creates a single-node swarm
on the current node.

The Engine sets up the swarm as follows:

· switches the current node into swarm mode.

· creates a swarm named default.

· designates the current node as a leader manager node for the swarm.

· names the node with the machine hostname.

· configures the manager to listen on an active network interface on
port 2377.

· sets the current node to Active availability, meaning it can receive
tasks from the scheduler.

· starts an internal distributed data store for Engines participating in
the swarm to maintain a consistent view of the swarm and all services
running on it.

· by default, generates a self-signed root CA for the swarm.

· by default, generates tokens for worker and manager nodes to join the
swarm.

· creates an overlay network named ingress for publishing service ports
external to the swarm.

· creates an overlay default IP addresses and subnet mask for your
networks

The output for docker swarm init provides the connection command to use
when you join new worker nodes to the swarm

<https://docs.docker.com/engine/swarm/swarm-mode/#create-a-swarm>

#### Answer 67: a

Explanation:

A **ConfigMap** is an API object used to store non-confidential data in
key-value pairs. Pods can consume ConfigMaps as environment variables,
command-line arguments, or as configuration files in a volume.

A ConfigMap allows you to decouple environment-specific configuration
from your container images, so that your applications are easily
portable.

Use a ConfigMap for setting configuration data separately from the
application code.

For example, imagine that you are developing an application that you can
run on your own computer (for development) and in the cloud (to handle
real traffic). You write the code to look in an environment variable
named DATABASE_HOST. Locally, you set that variable to localhost. In the
cloud, you set it to refer to a Kubernetes Service that exposes the
database component to your cluster.

<https://kubernetes.io/docs/concepts/configuration/configmap/#motivation>

#### Answer 68: c

Explanation:

Don\'t use naked Pods (that is, Pods not bound to a ReplicaSet or
Deployment) if you can avoid it. Naked Pods will not be rescheduled in
the event of a node failure.

A **Deployment**, which both creates a **ReplicaSet** to ensure that the
desired number of Pods is always available and specifies **a strategy to
replace Pods** (such as RollingUpdate), is almost always preferable to
creating Pods directly, except for some explicit restartPolicy: Never
scenarios. A Job may also be appropriate.

<https://kubernetes.io/docs/concepts/configuration/overview/#naked-pods-vs-replicasets-deployments-and-jobs>

A ReplicaSet ensures that a specified number of pod replicas are running
at any given time. However, a Deployment is a higher-level concept that
manages ReplicaSets and provides declarative updates to Pods along with
a lot of other useful features. Therefore, we recommend using
Deployments instead of directly using ReplicaSets, unless you require
custom update orchestration or don\'t require updates at all.

This actually means that you may never need to manipulate ReplicaSet
objects: use a Deployment instead, and define your application in the
spec section.

<https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#when-to-use-a-replicaset>

#### Answer 69: c

Explanation:

    docker node inspect self --pretty

You can run docker node inspect \<NODE-ID\> on a manager node to view
the details for an individual node. The output defaults to JSON format,
but you can pass the \--pretty flag to print the results in
human-readable format.

<https://docs.docker.com/engine/swarm/manage-nodes/#inspect-an-individual-node>

    docker node ls [OPTIONS]

Lists all the nodes that the Docker Swarm manager knows about. This is a
cluster management command and must be executed on a **swarm manager
node**. To learn about managers and workers, refer to the Swarm mode
section in the documentation.

<https://docs.docker.com/engine/reference/commandline/node_ls/>

#### Answer 70: c

Explanation:

You can change almost everything about an existing service using
the docker service update command.

Use the \--network-add or \--network-rm flags to add or remove a network
for a service.

Assuming that the my_web service from the previous section still exists,
use the following command to add a network:

    $ docker service update --network-add

<https://docs.docker.com/engine/reference/commandline/service_update/#add-or-remove-network>

#### Answer 71: b

Explanation:

When Docker is running in swarm mode, you can still run standalone
containers on any of the Docker hosts participating in the swarm, as
well as swarm services.

A key difference between standalone containers and swarm services is
that only swarm managers can manage a swarm, while standalone containers
can be started on any daemon. Docker daemons can participate in a swarm
as managers, workers, or both.

One of the key advantages of swarm services over standalone containers
is that you can modify a service's configuration, including the networks
and volumes it is connected to, without the need to manually restart the
service. Docker will update the configuration, stop the service tasks
with the out of date configuration, and create new ones matching the
desired configuration.

<https://docs.docker.com/engine/swarm/key-concepts/>

#### Answer 72: c

Explanation:

To configure the restart policy for a container, use the \--restart flag
when using the docker run command. The value of the \--restart flag can
be any of the following:

· **no** - Do not automatically restart the container. (the default)

· **on-failure** - Restart the container if it exits due to an error,
which manifests as a non-zero exit code.

· **always** - Always restart the container if it stops. If it is
manually stopped, it is restarted only when Docker daemon restarts or
the container itself is manually restarted. (See the second bullet
listed in restart policy details)

· **unless-stopped** - Similar to always, except that when the container
is stopped (manually or otherwise), it is not restarted even after
Docker daemon restarts.

<https://docs.docker.com/config/containers/start-containers-automatically/>

#### Answer 73: a, b, d

Explanation:

The following are typical use cases for Deployments:

· Create a Deployment to **rollout a ReplicaSet**. The ReplicaSet
creates Pods in the background. Check the status of the rollout to see
if it succeeds or not.

· **Declare the new state of the Pods** by updating the PodTemplateSpec
of the Deployment. A new ReplicaSet is created and the Deployment
manages moving the Pods from the old ReplicaSet to the new one at a
controlled rate. Each new ReplicaSet updates the revision of the
Deployment.

· Rollback to an earlier Deployment revision if the current state of the
Deployment is not stable. Each rollback updates the revision of the
Deployment.

· **Scale up** the Deployment to facilitate more load.

· Pause the Deployment to apply multiple fixes to its PodTemplateSpec
and then resume it to start a new rollout.

· Use the status of the Deployment as an indicator that a rollout has
stuck.

· Clean up older ReplicaSets that you don\'t need anymore.

<https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#use-case>

Like a Deployment, a StatefulSet manages Pods that are based on an
identical container spec. Unlike a Deployment, a StatefulSet maintains a
sticky identity for each of their Pods. These pods are created from the
same spec, but are not interchangeable: each has a persistent identifier
that it maintains across any rescheduling.

<https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/>

#### Answer 74: a

Explanation:

**Maintain the quorum of managers**

If the swarm loses the quorum of managers, the swarm cannot perform
administrative tasks such
as **scaling** or **updating** **services** and **joining** or **removing** **nodes** from
the swarm.

Nevertheless, tasks on existing worker nodes continue to run.

<https://docs.docker.com/engine/swarm/admin_guide/#maintain-the-quorum-of-managers>

#### Answer 75: d

Explanation:

To remove one or more services from the swarm use:

    docker service rm SERVICE [SERVICE...]

*Note: This is a cluster management command, and must be executed on a
swarm manager node.*

<https://docs.docker.com/engine/reference/commandline/service_rm/>

#### Answer 76: b

Explanation:

You can print the inspect output in a human-readable format instead of
the default JSON output, by using the \--pretty option:

    docker service inspect --pretty serviceName

<https://docs.docker.com/engine/reference/commandline/service_inspect/#formatting>

#### Answer 77: a

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

<https://docs.docker.com/engine/swarm/services/#control-service-placement>

#### Answer 78: d

Explanation:

PLACEMENT CONSTRAINTS

Use placement constraints to control the nodes a service can be assigned
to.

In the following example, the service only runs on nodes with the label
region set to east. If no appropriately-labeled nodes are available,
tasks will wait in Pending until they become available.

    $ docker service create \

    --name my-nginx \

    --replicas 5 \

    --constraint node.labels.region==east \

    nginx

<https://docs.docker.com/engine/swarm/services/#control-service-placement>

#### Answer 79: b

Explanation:

There is no limit on the number of manager nodes.

The decision about how many manager nodes to implement is **a
trade-off** between **performance** and **fault-tolerance**.

Adding manager nodes to a swarm makes the swarm more fault-tolerant.
However, additional manager nodes reduce write performance because more
nodes must acknowledge proposals to update the swarm state. This means
more network round-trip traffic.

<https://docs.docker.com/engine/swarm/admin_guide/#operate-manager-nodes-in-a-swarm>

#### Answer 80: a

Explanation:

By default, a container has no resource constraints and can use as much
of a given resource as the host's kernel scheduler allows. Docker
provides ways to control how much memory, or CPU a container can use,
setting runtime configuration flags of the docker run command.

<https://docs.docker.com/config/containers/resource_constraints/#memory>

#### Answer 81: c

Explanation:

To fetch the logs of a container use:

    docker logs [OPTIONS] CONTAINER

The output might look like this:

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/containerLogs.png)

The docker logs command batch-retrieves logs present at the time of
execution.

<https://docs.docker.com/engine/reference/commandline/logs/>

#### Answer 82: a

Explanation:

Using Secrets as environment variables

To use a secret in an environment variable in a Pod:

· Create a secret or use an existing one. Multiple Pods can reference
the same secret.

· Modify your Pod definition in each container that you wish to consume
the value of a secret key to add an environment variable for each secret
key you wish to consume. The environment variable that consumes the
secret key should populate the secret\'s name and key in
env\[\].valueFrom.secretKeyRef.

· Modify your image and/or command line so that the program looks for
values in the specified environment variables.

This is an example of a Pod that uses secrets from environment
variables:

    apiVersion: v1

    kind: Pod

    metadata:

      name: secret-env-pod

    spec:

      containers:

      - name: mycontainer

        image: redis

        env:

          - name: SECRET_USERNAME

            valueFrom:

              secretKeyRef:

                name: mysecret

                key: username

<https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-environment-variables>

#### Answer 83: d

Explanation:

When the Docker Engine runs in swarm mode, manager nodes implement
the **Raft Consensus Algorithm** to manage the global cluster state.

Raft requires a majority of managers, also called the quorum, to agree
on proposed updates to the swarm, such as node additions or removals.

<https://docs.docker.com/engine/swarm/admin_guide/#operate-manager-nodes-in-a-swarm>

If the swarm loses the quorum of managers, the swarm cannot perform
administrative tasks such as scaling or updating services and joining or
removing nodes from the swarm.

Nevertheless, tasks on existing worker nodes continue to run.

Raft tolerates up to **(N - 1)/2 failures** and requires a majority or
quorum of** (N/2) + 1** members to agree on values proposed to the
cluster. This means that in a cluster of 5 Managers running Raft, if 3
nodes are unavailable, the system cannot process any more requests to
schedule additional tasks. The existing tasks keep running but the
scheduler cannot rebalance tasks to cope with failures if the manager
set is not healthy.

<https://docs.docker.com/engine/swarm/raft/>

![outputDockerps](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/raft.jpg)

#### Answer 84: b

Explanation:

Docker provides **restart policies** to control whether your containers
start automatically when they exit, or when Docker restarts. Restart
policies ensure that linked containers are started in the correct order.
Docker recommends that you use restart policies, and avoid using process
managers to start containers.

Restart policies only apply to containers. Restart policies for swarm
services are configured differently using other flags related
to **service restart.**

<https://docs.docker.com/config/containers/start-containers-automatically/#restart-policy-details>

<https://docs.docker.com/engine/reference/run/#restart-policies---restart>
