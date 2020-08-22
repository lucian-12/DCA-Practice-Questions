### **Answer 1: b**

*Explanation*

Different types and use cases for the built-in network drivers:

· **User-defined bridge networks** are best when you need multiple
containers to communicate on the same Docker host.

· **Host networks** are best when the network stack should not be
isolated from the Docker host, but you want other aspects of the
container to be isolated.

· **Overlay networks** are best when you need containers running on
different Docker hosts to communicate, or when multiple applications
work together using swarm services.

· **Macvlan networks** are best when you are migrating from a VM setup
or need your containers to look like physical hosts on your network,
each with a unique MAC address.

· **Third-party network** plugins allow you to integrate Docker with
specialized network stacks.

https://docs.docker.com/network/#network-driver-summary\#network-driver-summary

### **Answer 2: b**

*Explanation*

To publish all ports, use the -P flag. For example, the following
command starts a container (in detached mode) and the -P flag publishes
all exposed ports of the container to random ports on the
host **interfaces**.

    $ docker run -d -P --name webserver nginx

[[https://docs.docker.com/config/containers/container-networking/]{.ul}](https://docs.docker.com/config/containers/container-networking/)

### **Answer 3: b**

*Explanation*

**Linked containers on the default bridge network share environment
variables.**

First, \--link option, which is considered legacy.

Originally, the only way to share environment variables between two
containers was to link them using the \--link flag. This type of
variable sharing is **not possible with user-defined
networks.** However, there are superior ways to share environment
variables. A few ideas:

are file or directory mounting, use docker-compose, secrets and
configmaps.

**User-defined bridges provide better isolation.**

All containers without a \--network specified, are attached to the
default bridge network. This can be a risk, as unrelated
stacks/services/containers are then able to communicate.

Using a user-defined network provides a scoped network in which only
containers attached to that network are able to communicate.

**Containers can be attached and detached from user-defined networks on
the fly.**

**Each user-defined network creates a configurable bridge**

User-defined bridge networks are created and configured using docker
network create. If different groups of applications have different
network requirements, you can configure each user-defined bridge
separately, as you create it.

[[https://docs.docker.com/network/bridge/]{.ul}](https://docs.docker.com/network/bridge/)

### **Answer 4: a**

*Explanation*

The swarm mode routing mesh is great for transport-layer routing. It
routes to services using the service\'s published ports.

However, if you want to route traffic to services based on hostname
instead you have to use the \"**Swarm Layer 7 Routing **(Interlock)\".

This is a feature that enables service discovery on the application
layer (L7). This Layer 7 Routing extends upon the swarm mode routing
mesh by adding application layer capabilities such as inspecting the
HTTP header.

The Interlock Proxy works by using the HTTP/1.1 header field definition.
Every HTTP/1.1 TCP request contains a Host: header.

[[https://success.docker.com/article/ucp-service-discovery-swarm\#interlockproxyusageexamples]{.ul}](https://success.docker.com/article/ucp-service-discovery-swarm#interlockproxyusageexamples)

### **Answer 5: b**

*Explanation*

Internal Load Balancing

When services are created in a Docker swarm cluster, they are
automatically assigned a Virtual IP (VIP) that is part of the service\'s
network. The VIP is returned when resolving the service\'s name.

Traffic to the VIP is automatically sent to all healthy tasks of that
service across the overlay network. This approach avoids any client-side
load balancing because only a single IP is returned to the client.
Docker takes care of routing and equally distributes the traffic across
the healthy service tasks.

[[https://success.docker.com/article/ucp-service-discovery-swarm\#interlockproxyusageexamples]{.ul}](https://success.docker.com/article/ucp-service-discovery-swarm#interlockproxyusageexamples)

### **Answer 6: d**

*Explanation*

The **overlay network driver** creates a distributed network among
multiple Docker daemon hosts.

This network sits on top of (overlays) the host-specific networks,
allowing containers connected to it (including swarm service containers)
to communicate securely when encryption is enabled.

Docker transparently handles routing of each packet to and from the
correct Docker daemon host and the correct destination container.

[[https://docs.docker.com/network/overlay/]{.ul}](https://docs.docker.com/network/overlay/)

### **Answer 7: a, d**

*Explanation*

Kubernetes supports two primary modes of finding a Service, environment
variables(injected by the kubelet when pods are created) and DNS. Both
are valid options, however, the most common method to discover and reach
a service from within Docker Kubernetes Service is to use the embedded
DNS service.

[[https://kubernetes.io/docs/concepts/services-networking/service/\#discovering-services]{.ul}](https://kubernetes.io/docs/concepts/services-networking/service/#discovering-services)

### **Answer 8: b**

*Explanation*

If you use the **host network** mode for a container, that container's
network stack is not isolated from the Docker host (the container shares
the host's networking namespace), and the container does not get its own
IP-address allocated.

https://docs.docker.com/network/host/

Host networks are best when the network stack should not be isolated
from the Docker host, but you want other aspects of the container to be
isolated.

https://docs.docker.com/network/#network-driver-summary

### **Answer 9: a, c, d**

*Explanation*

Docker port command only shows the port published externally.

[[https://docs.docker.com/engine/reference/commandline/port/]{.ul}](https://docs.docker.com/engine/reference/commandline/port/)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/portsMapped.png)


### **Answer 10: b**

*Explanation*

**Using a user-defined network** provides a scoped network in which only
containers attached to that network are able to communicate.

Furthermore, on user-defined networks, containers can not only
communicate by IP address, but can also resolve a container name to an
IP address. This capability is called automatic service discovery.

[[https://docs.docker.com/network/network-tutorial-standalone/\#use-user-defined-bridge-networks]{.ul}](https://docs.docker.com/network/network-tutorial-standalone/#use-user-defined-bridge-networks)

However, containers connected to the **default bridge network** can
communicate, but only by IP address, unless they are linked using the
legacy \--link flag.

Obs. If you do not specify a network using the \--network flag, and you
do specify a network driver, your container is connected to the default
bridge network by default.

[[https://docs.docker.com/network/bridge/\#connect-a-container-to-the-default-bridge-network]{.ul}](https://docs.docker.com/network/bridge/#connect-a-container-to-the-default-bridge-network)

### **Answer 11: c**

*Explanation*

Services will receive a cluster-scoped Virtual IP address also known as
ClusterIP.

**ClusterIP** is the default method of exposing the service internally.
Once the service is created and a VIP is associated with it, every
kube-proxy running on every cluster node will program an iptables rule
so that all traffic destined to that VIP will be redirected to one of
the Service's backend pods instead.

If the service needs to be accessed from outside the cluster, then there
are a couple of available options to doing so. Mainly NodePort and
LoadBalancer.

Ingress is another method that you can use. Ingress is technically not a
Type of a service, but it\'s another method for using Layer 7 based
routing to expose your services externally.

[[https://success.docker.com/article/ucp-service-discovery-k8s]{.ul}](https://success.docker.com/article/ucp-service-discovery-k8s)

### **Answer 12: c**

*Explanation*

To create a new network use:

    docker network create [OPTIONS] NETWORK

For example:

    $ docker network create -d bridge my-bridge-network

The DRIVER accepts bridge or overlay which are the built-in network
drivers. If you have installed a third party or your own custom network
driver you can specify that DRIVER here also. If you don't specify
the \--driver option, the command automatically creates a bridge network
for you.

[[https://docs.docker.com/engine/reference/commandline/network_create/]{.ul}](https://docs.docker.com/engine/reference/commandline/network_create/)

### **Answer 13: a**

*Explanation*

Docker Engine swarm mode makes it easy to publish ports for services to
make them available to resources outside the swarm.

All nodes participate in an ingress routing mesh.

The routing mesh **enables each node in the swarm to accept connections
on published ports** for any service running in the swarm, even if
there's no task running on the node.

The routing mesh routes all incoming requests to published ports on
available nodes to an active container.

[[https://docs.docker.com/engine/swarm/ingress/]{.ul}](https://docs.docker.com/engine/swarm/ingress/)

### **Answer 14: b**

*Explanation*

**Encrypt traffic on an overlay network**

All swarm service management traffic is encrypted by default, using the
AES algorithm in GCM mode. Manager nodes in the swarm rotate the key
used to encrypt gossip data every 12 hours.

To encrypt application data as well, add \--opt encrypted when creating
the overlay network. This enables IPSEC encryption at the level of the
vxlan. This encryption imposes a non-negligible performance penalty, so
you should test this option before using it in production.

[[https://docs.docker.com/network/overlay/]{.ul}](https://docs.docker.com/network/overlay/)

To set driver specific options use: \--opt , -o

For example:

    $ docker network create -d overlay \

      --opt encrypted=true \

      my-network -network

[[https://docs.docker.com/engine/reference/commandline/network_create/]{.ul}](https://docs.docker.com/engine/reference/commandline/network_create/)

### **Answer 15: b**

*Explanation*

To create an overlay network which can be used by swarm services or
standalone containers to communicate with other standalone containers
running on other Docker daemons, add the \--attachable flag:

    $ docker network create -d overlay --attachable my-attachable-overlay

[[https://docs.docker.com/network/overlay/]{.ul}](https://docs.docker.com/network/overlay/)

### **Answer 16: d**

*Explanation*

To start a container in detached mode, you use -d=true or
just -d option. By design, containers started in detached mode exit when
the root process used to run the container exits.

[[https://docs.docker.com/engine/reference/run/\#detached\--d]{.ul}](https://docs.docker.com/engine/reference/run/#detached--d)

To make a port available to services outside of Docker, or to Docker
containers which are not connected to the container's network, use
the \--publish or -p flag.

Here is anexample:

    docker run -p 80:8080 ubuntu bash

This binds port 8080 of the container to TCP port 80 on the host
machine.

[[https://docs.docker.com/engine/reference/commandline/run/\#publish-or-expose-port\--p\-\--expose]{.ul}](https://docs.docker.com/engine/reference/commandline/run/#publish-or-expose-port--p---expose)

[[https://docs.docker.com/config/containers/container-networking/\#published-ports]{.ul}](https://docs.docker.com/config/containers/container-networking/#published-ports)

### **Answer 17: d**

*Explanation*

If you do not specify a network using the \--network flag, and you do
specify a network driver, your container is connected to the default
bridge network by default.

[[https://docs.docker.com/network/bridge/\#use-the-default-bridge-network]{.ul}](https://docs.docker.com/network/bridge/#use-the-default-bridge-network)

### **Answer 18: d**

*Explanation*

The ingress network is created without the \--attachable flag, which
means that only swarm services can use it, and not standalone
containers.

You can connect standalone containers to user-defined overlay networks
which are created with the \--attachable flag.

[[https://docs.docker.com/network/overlay/\#attach-a-standalone-container-to-an-overlay-network]{.ul}](https://docs.docker.com/network/overlay/#attach-a-standalone-container-to-an-overlay-network)

The routing mesh allows all the swarm nodes to accept connections on the
services published ports. When any swarm node receives traffic destined
to the published TCP/UDP port of a running service, it forwards the
traffic to the service\'s VIP using a pre-defined overlay network
called **ingress**. The ingress network behaves similarly to other
overlay networks, but its sole purpose is to transport mesh routing
traffic from external clients to cluster services. It uses the same
VIP-based internal load balancing as described in the previous section.

[[https://success.docker.com/article/ucp-service-discovery-swarm\#interlockproxyusageexamples]{.ul}](https://success.docker.com/article/ucp-service-discovery-swarm#interlockproxyusageexamples)

### **Answer 19: c**

*Explanation*

Ingress is one of the types of **overlay networks**, which sits on top
of (overlays) the host-specific networks and handles control and data
traffic related to swarm services.

[[https://docs.docker.com/network/overlay/\#customize-the-default-ingress-network]{.ul}](https://docs.docker.com/network/overlay/#customize-the-default-ingress-network)

### **Answer 20: b**

*Explanation*

The following run command options work with container networking:

    --publish-all or -P

Publish all exposed ports to the host **interfaces**. Docker binds each
exposed port to a random port on the host. Use the -p flag to explicitly
map a single port or range of ports.

    -p or --publish

It makes a port available to services outside of Docker, or to Docker
containers which are not connected to the container's network.

    format: ip:hostPort:containerPort | ip::containerPort |
    hostPort:containerPort | containerPort

[[https://docs.docker.com/engine/reference/run/\#expose-incoming-ports]{.ul}](https://docs.docker.com/engine/reference/run/#expose-incoming-ports)

[[https://docs.docker.com/config/containers/container-networking/]{.ul}](https://docs.docker.com/config/containers/container-networking/)

### **Answer 21: d**

*Explanation*

Docker Universal Control Plane (UCP) uses Calico as the default
Kubernetes networking solution. Calico is configured to create a Border
Gateway Protocol (BGP) mesh between all nodes in the cluster.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 22: c, e**

*Explanation*

Docker uses embedded DNS to provide **service discovery** for containers
running on a single Docker engine and tasks running in a Docker swarm.

The Docker engine checks if the DNS query belongs to a container or
service on each network that the requesting container belongs to. If it
does, then the Docker engine looks up the IP address that matches the
name of a container, task, or service in a key-value store and returns
that IP or service **Virtual IP** (VIP) back to the requester. Here, all
nodes participate in a network called routing mesh.

[[https://success.docker.com/article/ucp-service-discovery-swarm]{.ul}](https://success.docker.com/article/ucp-service-discovery-swarm)

**DNS round robin** (DNS RR) load balancing is another load balancing
option for services (configured with \--endpoint-mode dnsrr). In DNS RR
mode a VIP is not created for each service. The Docker DNS server
resolves a service name to individual container IPs in round robin
fashion.

[[https://success.docker.com/article/networking]{.ul}](https://success.docker.com/article/networking)

To use an external load balancer without the routing mesh, set
\--endpoint-mode to dnsrr instead of the default value of vip.

In this case, there is not a single virtual IP. Instead, Docker sets up
DNS entries for the service such that a DNS query for the service name
returns a list of IP addresses, and the client connects directly to one
of these. You are responsible for providing the list of IP addresses and
ports to your load balancer. See Configure service discovery.

[[https://docs.docker.com/engine/swarm/ingress/\#without-the-routing-mesh]{.ul}](https://docs.docker.com/engine/swarm/ingress/#without-the-routing-mesh)

### **Answer 23: c**

*Explanation*

When you initialize a swarm or join a Docker host to an existing swarm,
two new networks are created on that Docker host:

· an overlay network called **ingress**, which handles control and data
traffic related to swarm services. When you create a swarm service and
do not connect it to a user-defined overlay network, it connects to the
ingress network by default.

· a bridge network called **docker_gwbridge**, which connects the
individual Docker daemon to the other daemons participating in the
swarm.

[[https://docs.docker.com/network/overlay/]{.ul}](https://docs.docker.com/network/overlay/)

### **Answer 24: b**

*Explanation*

When creating overlay networks, the are some prerequisites:

· Setup the firewall rules

You need the following ports open to traffic to and from each Docker
host participating on an overlay network:

TCP port 2377 for cluster management communications

TCP and UDP port 7946 for communication among nodes

UDP port 4789 for overlay network traffic

· Before you can create an overlay network, you need to either
initialize your Docker daemon as a swarm manager using docker swarm init
or join it to an existing swarm using docker swarm join. Either of these
creates the default ingress overlay network which is used by swarm
services by default. You need to do this even if you never plan to use
swarm services. Afterward, you can create additional user-defined
overlay networks.

[[https://docs.docker.com/network/overlay/\#operations-for-all-overlay-networks]{.ul}](https://docs.docker.com/network/overlay/#operations-for-all-overlay-networks)

### **Answer 25: b**

*Explanation*

**Linux bridges** only operate locally and cannot span across nodes.

So, for multi-host networking we need another mechanism.
Linux **VXLAN** comes to the rescue.

When a container sends a data packet, the bridge realizes that the
target of the packet is not on this host.

Now, each node participating in an overlay network gets a so-called
VXLAN Tunnel Endpoint (VTEP) object, which intercepts the packet (the
packet at that moment is an OSI layer 2 data packet), wraps it with a
header containing the target IP address of the host that runs the target
container (this makes it now an OSI layer 3 data packet), and sends it
over the VXLAN tunnel.

The VTEP on the other side of the tunnel unpacks the data packet and
forwards it to the local bridge, which in turn forwards it to the target
container.

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/VXLAN_tunnel.jpg)

### **Answer 26: d**

*Explanation*

To manage networks, you can use:

    docker network COMMAND

To display detailed information on one or more networks you can use:

    docker network inspect [OPTIONS] NETWORK [NETWORK...]

[[https://docs.docker.com/engine/reference/commandline/network_inspect/]{.ul}](https://docs.docker.com/engine/reference/commandline/network_inspect/)

### **Answer 27: d**

*Explanation*

The following run command options work with container networking:

    --expose

Expose a port or a range of ports inside the container. You expose ports
using the EXPOSE keyword in the Dockerfile or the \--expose flag to
docker run. Exposing ports is a way of **documenting** which ports are
used, but **does not actually map or open any ports**. Exposing ports is
optional.

    --publish-all or -P

Publish all exposed ports to the host **interfaces**. Docker binds each
exposed port to a random port on the host. Use the -p flag to explicitly
map a single port or range of ports.

    -p or --publish

It makes a port available to services outside of Docker, or to Docker
containers which are not connected to the container's network.

    format: ip:hostPort:containerPort | ip::containerPort |
    hostPort:containerPort | containerPort

[[https://docs.docker.com/engine/reference/run/\#expose-incoming-ports]{.ul}](https://docs.docker.com/engine/reference/run/#expose-incoming-ports)

[[https://docs.docker.com/config/containers/container-networking/]{.ul}](https://docs.docker.com/config/containers/container-networking/)

Example:

docker run -p 127.0.0.1:80:8080 ubuntu bash

### **Answer 28: a, d**

*Explanation*

When you create a **macvlan** **network**, it can either be in bridge
mode or 802.1q trunk bridge mode.

· In bridge mode, macvlan traffic goes through a physical device on the
host.

· In 802.1q trunk bridge mode, traffic goes through an 802.1q
sub-interface which Docker creates on the fly. This allows you to
control routing and filtering at a more granular level.

https://docs.docker.com/network/macvlan/#create-a-macvlan-network

### **Answer 29: b**

*Explanation*

The following run command options work with container networking:

    --expose

Expose a port or a range of ports inside the container. You expose ports
using the EXPOSE keyword in the Dockerfile or the \--expose flag to
docker run. Exposing ports is a way of **documenting** which ports are
used, but **does not actually map or open any ports**. Exposing ports is
optional.

    --publish-all or -P

Publish all exposed ports to the host **interfaces**. Docker binds each
exposed port to a random port on the host. Use the -p flag to explicitly
map a single port or range of ports.

    -p or --publish

It makes a port available to services outside of Docker, or to Docker
containers which are not connected to the container's network.

    format: ip:hostPort:containerPort | ip::containerPort |
    hostPort:containerPort | containerPort

[[https://docs.docker.com/engine/reference/run/\#expose-incoming-ports]{.ul}](https://docs.docker.com/engine/reference/run/#expose-incoming-ports)

[[https://docs.docker.com/config/containers/container-networking/]{.ul}](https://docs.docker.com/config/containers/container-networking/)

### **Answer 30: d**

*Explanation*

Network Scope

Docker network drivers have a concept of **scope**. The network scope is
the domain of the driver which can be the local or swarm scope.

**Local scope** drivers provide connectivity and network services (such
as DNS or IPAM) within the scope of the host.

**Swarm scope** drivers provide connectivity and network services across
a swarm cluster. Swarm scope networks have the same network ID across
the entire cluster while local scope networks have a unique network ID
on each host.

[[https://success.docker.com/article/networking\#networkscope]{.ul}](https://success.docker.com/article/networking#networkscope)

You can check this by running:

    $ docker network ls

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/networkLS.png)

### **Answer 31: d**

*Explanation*

By using dockerd you can start the Docker daemon manually. On a typical
installation the Docker daemon is started by a system utility, not
manually by a user. However, this command can be useful to test things
out and for troubleshooting problems.

To configure the DNS servers for all Docker containers you have to set
the configuration at Docker daemon level.

By using dockerd command you can also configure it using flags.

For example, to set the DNS server for all Docker containers, use:

    dockerd --dns IP_ADDRESS

To specify multiple DNS servers, use multiple \--dns flags.

If the container cannot reach any of the IP addresses you specify,
Google's public DNS server 8.8.8.8 is added, so that your container can
resolve internet domains.

[[http://dockerlabs.collabnix.com/beginners/components/daemon/]{.ul}](http://dockerlabs.collabnix.com/beginners/components/daemon/)

[[https://docs.docker.com/config/containers/container-networking/]{.ul}](https://docs.docker.com/config/containers/container-networking/)

### **Answer 32: a**

*Explanation*

When you create a swarm service, you can publish that service's ports to
hosts outside the swarm in two ways:

· You can rely on the **routing mesh**. When you publish a service port,
the swarm makes the service accessible at the target port on every node,
regardless of whether there is a task for the service running on that
node or not. This is less complex and is the right choice for many types
of services.

· You can publish a service task's port directly on the swarm node where
that service is running. This feature is available in Docker 1.13 and
higher. This bypasses the routing mesh and provides the maximum
flexibility, including the ability for you to develop your own routing
framework. However, you are responsible for keeping track of where each
task is running and routing requests to the tasks, and load-balancing
across the nodes.

By default, services are using the routing mesh which makes the service
accessible at the published port on every swarm node. When a user or
process connects to a service, any worker node running a service task
may respond.

To publish a service's port directly on the node where it is running,
use the mode=host option to the \--publish flag.

For example:

    $ docker service create \

      --mode global \

      --publish mode=host,target=80,published=8080 \

      --name=nginx \

      nginx:latest

[[https://docs.docker.com/engine/swarm/services/\#publish-ports]{.ul}](https://docs.docker.com/engine/swarm/services/#publish-ports)

### **Answer 33: a**

*Explanation*

**Bridge networks** apply to containers running on the same Docker
daemon host.

When you start Docker, a default bridge network (also called bridge) is
created automatically, and newly-started containers connect to it unless
otherwise specified.

You can also create user-defined custom bridge networks. User-defined
bridge networks are superior to the default bridge network for the
following reasons:

· User-defined bridges provide automatic DNS resolution between
containers.

· User-defined bridges provide better isolation.

· Containers can be attached and detached from user-defined networks on
the fly.

· Each user-defined network creates a configurable bridge.

· Linked containers on the default bridge network share environment
variables.

[[https://docs.docker.com/network/bridge/\#differences-between-user-defined-bridges-and-the-default-bridge]{.ul}](https://docs.docker.com/network/bridge/#differences-between-user-defined-bridges-and-the-default-bridge)

### **Answer 34: c**

*Explanation*

IPAM Drivers --- Docker has a native IP Address Management Driver that
provides default subnets or IP addresses for the networks and endpoints
if they are not specified. IP addressing can also be manually assigned
through network, container, and service create commands. Remote IPAM
drivers also exist and provide integration to existing IPAM tools.

[[https://success.docker.com/article/networking\#networkscope]{.ul}](https://success.docker.com/article/networking#networkscope)

### **Answer 35: d**

*Explanation*

If you use the **host network** mode for a container, that container's
network stack is not isolated from the Docker host (the container shares
the host's networking namespace), and the container does not get its own
IP-address allocated.

https://docs.docker.com/network/host/

Host networks are best when the network stack should not be isolated
from the Docker host, but you want other aspects of the container to be
isolated.

https://docs.docker.com/network/#network-driver-summary

### **Answer 36: c**

*Explanation*

If you use the **host network** mode for a container, that container's
network stack is not isolated from the Docker host (the container shares
the host's networking namespace), and the container does not get its own
IP-address allocated.

For instance, if you run a container which binds to port 80 and you use
host networking, the container's application is available on port 80 on
the host's IP address.

The host networking driver only works on Linux hosts, and is not
supported on Docker Desktop for Mac, Docker Desktop for Windows, or
Docker EE for Windows Server.

Host mode networking can be useful to optimize performance, and in
situations where a container needs to handle a large range of ports, as
it does not require network address translation (NAT), and no
"userland-proxy" is created for each port.

[[https://docs.docker.com/network/host/]{.ul}](https://docs.docker.com/network/host/)

### **Answer 37: a**

*Explanation*

There are several high-level constructs in the CNM. They are all OS and
infrastructure agnostic so that applications can have a uniform
experience no matter the infrastructure stack.

· **Sandbox** --- A Sandbox contains the configuration of a container\'s
network stack. This includes the management of the container\'s
interfaces, routing table, and DNS settings. An implementation of a
Sandbox could be a Windows HNS or Linux Network Namespace, a FreeBSD
Jail, or other similar concept. A Sandbox may contain many endpoints
from multiple networks.

· **Endpoint** --- An Endpoint joins a Sandbox to a Network. The
Endpoint construct exists so the actual connection to the network can be
abstracted away from the application. This helps maintain portability so
that a service can use different types of network drivers without being
concerned with how it\'s connected to that network.

· **Network** --- The CNM does not specify a Network in terms of the OSI
model. An implementation of a Network could be a Linux bridge, a VLAN,
etc. A Network is a collection of endpoints that have connectivity
between them. Endpoints that are not connected to a network do not have
connectivity on a network.

[[https://success.docker.com/article/networking\#cnmconstructs]{.ul}](https://success.docker.com/article/networking#cnmconstructs)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/dockerCNM.jpg)

### **Answer 38: b**

*Explanation*

Docker Engine swarm mode makes it easy to publish ports for services to
make them available to resources outside the swarm.

All nodes participate in an ingress routing mesh.

The routing mesh **enables each node in the swarm to accept connections
on published ports** for any service running in the swarm, even if
there's no task running on the node.

The routing mesh routes all incoming requests to published ports on
available nodes to an active container.

[[https://docs.docker.com/engine/swarm/ingress/]{.ul}](https://docs.docker.com/engine/swarm/ingress/)

### **Answer 39: c**

*Explanation*

By default, a container inherits the DNS settings of the Docker daemon.

To specify a DNS server for an individual container use:

    docker container create --dns=IP_ADDRESS

To specify multiple DNS servers, use multiple \--dns flags. If the
container cannot reach any of the IP addresses you specify, Google's
public DNS server 8.8.8.8 is added, so that your container can resolve
internet domains.

[[https://docs.docker.com/config/containers/container-networking/\#dns-services]{.ul}](https://docs.docker.com/config/containers/container-networking/#dns-services)

### **Answer 40: d**

*Explanation*

The **sandbox** perfectly isolates a container from the outside world.
No inbound network connection is allowed into the sandboxed container.
Yet, it is very unlikely that a container will be of any value in a
system if absolutely no communication with it is possible. To work
around this, we have element number two, which is the endpoint.

An endpoint is a **controlled** gateway from the outside world into the
network\'s sandbox that shields the container. The endpoint connects the
network sandbox, but not the container, to the third element of the
model, which is the network. Also, the Endpoint construct exists so
the **actual** connection to the network can be **abstracted away from
the application**. This helps **maintain portability** so that a service
can use different types of network drivers without being concerned with
how it\'s connected to that network.

[[https://success.docker.com/article/networking\#networkscope]{.ul}](https://success.docker.com/article/networking#networkscope)

### **Answer 41: d**

*Explanation*

NodePort service type is well suited for application services that
require direct TCP/UDP access, like RabbitMQ for example.

If your service can be accessed using HTTP/HTTPs then Ingress is
recommended.

Ingress is a Kubernetes API object that manages external access to the
services in a cluster, typically HTTP/HTTPS.

[[https://success.docker.com/article/ucp-service-discovery-k8s]{.ul}](https://success.docker.com/article/ucp-service-discovery-k8s)

[[https://www.docker.com/blog/designing-your-first-application-kubernetes-communication-services-part3/]{.ul}](https://www.docker.com/blog/designing-your-first-application-kubernetes-communication-services-part3/)

### **Answer 42: a**

*Explanation*

The **overlay network driver** creates a distributed network among
multiple Docker daemon hosts. This network sits on top of (overlays) the
host-specific networks, allowing containers connected to it (including
swarm service containers) to communicate securely when encryption is
enabled. Docker transparently handles routing of each packet to and from
the correct Docker daemon host and the correct destination container.

[[https://docs.docker.com/network/overlay/]{.ul}](https://docs.docker.com/network/overlay/)

### **Answer 43: d**

*Explanation*

With the network set to host a container will share the host's network
stack and all interfaces from the host will be available to the
container.

The container's hostname will match the hostname on the host system.

Even in host network mode a container has its own UTS namespace by
default.

As such \--hostname and \--domainname are allowed in host network mode
and will only change the hostname and domain name inside the container.

[[https://docs.docker.com/engine/reference/run/#network-settings]{.ul}](https://docs.docker.com/engine/reference/run/#network-settings)

### **Answer 44: b**

*Explanation*

When you create a swarm service and do not connect it to a user-defined
overlay network, it connects to the **ingress network** by default.

[[https://docs.docker.com/network/overlay/]{.ul}](https://docs.docker.com/network/overlay/)

### **Answer 45: b**

*Explanation*

Different types and use cases for the built-in network drivers:

· **User-defined bridge networks** are best when you need multiple
containers to communicate on the same Docker host.

· **Host networks** are best when the network stack should not be
isolated from the Docker host, but you want other aspects of the
container to be isolated.

· **Overlay networks** are best when you need containers running on
different Docker hosts to communicate, or when multiple applications
work together using swarm services.

· **Macvlan networks** are best when you are migrating from a VM setup
or need your containers to look like physical hosts on your network,
each with a unique MAC address.

· **Third-party network** plugins allow you to integrate Docker with
specialized network stacks.

https://docs.docker.com/network/#network-driver-summary\#network-driver-summary

### **Answer 46: a**

*Explanation*

**macvlan**: Macvlan networks allow you to assign a MAC address to a
container, making it appear as a physical device on your network. The
Docker daemon routes traffic to containers by their MAC addresses. Using
the macvlan driver is sometimes the best choice when dealing with legacy
applications that expect to be directly connected to the physical
network, rather than routed through the Docker host's network stack. See
Macvlan networks.

https://docs.docker.com/network/#network-drivers

### **Answer 47: c**

*Explanation*

To connect a running container to an existing user-defined bridge, use
the docker network connect command.

The following command connects an already-running my-nginx container to
an already-existing my-net network:

    $ docker network connect my-net my-nginx

[[https://docs.docker.com/network/bridge/\#connect-a-container-to-a-user-defined-bridge]{.ul}](https://docs.docker.com/network/bridge/#connect-a-container-to-a-user-defined-bridge)

### **Answer 48: c**

*Explanation*

    docker network ls [OPTIONS]

Lists all the networks the Engine daemon knows about. This includes the
networks that span across multiple hosts in a cluster.

Example:

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/networkLS.png)

[[https://docs.docker.com/engine/reference/commandline/network_ls/]{.ul}](https://docs.docker.com/engine/reference/commandline/network_ls/)

### **Answer 49: b**

*Explanation*

Services using the routing mesh are running in virtual IP (VIP) mode.
Even a service running on each node (by means of the \--mode global
flag) uses the routing mesh. When using the routing mesh, there is no
guarantee about which Docker node services client requests.

To bypass the routing mesh, you can start a service using DNS Round
Robin (DNSRR) mode, by setting the \--endpoint-mode flag to dnsrr.

[[https://docs.docker.com/network/overlay/\#bypass-the-routing-mesh-for-a-swarm-service]{.ul}](https://docs.docker.com/network/overlay/#bypass-the-routing-mesh-for-a-swarm-service)

### **Answer 50: b**

*Explanation*

By default, Docker Swarm uses a default address pool 10.0.0.0/8 for
global scope (overlay) networks.

Every network that does not have a subnet specified will have a subnet
sequentially allocated from this pool. In some circumstances it may be
desirable to use a different default IP address pool for networks.

For example, if the default 10.0.0.0/8 range conflicts with already
allocated address space in your network, then it is desirable to ensure
that networks use a different range without requiring Swarm users to
specify each subnet with the \--subnet command.

[[https://docs.docker.com/engine/swarm/swarm-mode/\#configuring-default-address-pools]{.ul}](https://docs.docker.com/engine/swarm/swarm-mode/#configuring-default-address-pools)
