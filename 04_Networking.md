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

https://docs.docker.com/network/\#network-driver-summary\#network-driver-summary

### **Answer 2: b**

*Explanation*

To publish all ports, use the -P flag. For example, the following
command starts a container (in detached mode) and the -P flag publishes
all exposed ports of the container to random ports on the
host **interfaces**.

\$ docker run -d -P \--name webserver nginx

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

https://docs.docker.com/network/\#network-driver-summary

### **Answer 9: a, c, d**

*Explanation*

Docker port command only shows the port published externally.

[[https://docs.docker.com/engine/reference/commandline/port/]{.ul}](https://docs.docker.com/engine/reference/commandline/port/)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/portsMapped.png)
