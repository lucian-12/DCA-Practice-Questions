### **Answer 1: a**

*Explanation*

**Control groups**

Docker Engine on Linux also relies on another technology called control
groups (**cgroups**).

A cgroup limits an application to a specific set of resources. Control
groups allow Docker Engine to share available hardware resources to
containers and optionally enforce limits and constraints.

For example, you can limit the memory or CPU available to a specific
container.

[[https://docs.docker.com/get-started/overview/\#control-groups]{.ul}](https://docs.docker.com/get-started/overview/#control-groups)

### **Answer 2: b**

*Explanation*

By default, when the Docker daemon terminates, it shuts down running
containers. Starting with Docker Engine 1.12, you can configure the
daemon so that containers remain running if the daemon becomes
unavailable. This functionality is called live restore. The live restore
option helps reduce container downtime due to daemon crashes, planned
outages, or upgrades.

[[https://docs.docker.com/config/containers/live-restore/]{.ul}](https://docs.docker.com/config/containers/live-restore/)

### **Answer 3: b**

*Explanation*

\--default-ulimit allows you to set the default ulimit options to use
for all containers. It takes the same options as \--ulimit for docker
run. If these defaults are not set, ulimit settings will be inherited,
if not set on docker run, from the Docker daemon. Any \--ulimit options
passed to docker run will overwrite these defaults.

Be careful setting nproc with the ulimit flag as nproc is designed by
Linux to set the maximum number of processes available to a user, not to
a container. For details please check the run reference.

<https://docs.docker.com/engine/reference/commandline/dockerd/#default-ulimit-settings>

### **Answer 4: d**

*Explanation*

Linux **namespaces** provide isolation for running processes, limiting
their access to system resources without the running process being aware
of the limitations.

[[https://docs.docker.com/engine/security/userns-remap/]{.ul}](https://docs.docker.com/engine/security/userns-remap/)

Docker uses a this technology to provide the isolated workspace called
the container. When you run a container, Docker creates a set of
namespaces for that container.

These namespaces provide a layer of **isolation**. Each aspect of a
container runs in a separate namespace and its access is limited to that
namespace.

[[https://docs.docker.com/get-started/overview/\#namespaces]{.ul}](https://docs.docker.com/get-started/overview/#namespaces)

### **Answer 5: b**

*Explanation*

You can monitor the status of UCP either by using the web UI, either the
CLI.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 6: d**

*Explanation*

To backup the Swarm on Linux using Docker Engine \>= 17.03, you can use
the following steps.

Since this will need you to stop the engine of a manager, your cluster
need to be healthy with at least 3 managers.

1\. Select a manager node to do the operation. Try not to choose the
leader one in order to avoid a new election inside the cluster.

2\. Optional: Store the Docker version to a variable for easy addition
to your backup name.

3\. Stop the Docker Engine on the manager before backing up the data, so
that no data is being changed during the backup.

4\. Backup the entire Swarm folder /var/lib/docker/swarm.

5\. Restart the manager Docker Engine.

[[https://success.docker.com/article/backup-restore-swarm-manager]{.ul}](https://success.docker.com/article/backup-restore-swarm-manager)

Docker manager nodes store the swarm state and manager logs in the
/var/lib/docker/swarm/

[[https://docs.docker.com/engine/swarm/admin_guide/\#back-up-the-swarm]{.ul}](https://docs.docker.com/engine/swarm/admin_guide/#back-up-the-swarm)

\"/etc\" is used for configurations (.conf files etc). here you find all
the configs and settings for your system.

\"/var\" is usually used for log files, \'temporary\' files (like mail
spool, printer spool, etc), databases, and all other data not tied to a
specific user. Logs are usually in \"/var/log\", databases in
\"/var/lib\" (mysql - \"/var/lib/mysql\"), etc.

[[https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard]{.ul}](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)

### **Answer 7: d**

*Explanation*

Docker namespaces provide a layer of isolation. Each aspect of a
container runs in a separate namespace and its access is limited to that
namespace.

Docker Engine uses namespaces such as the following on Linux:

· The **pid** namespace: Process isolation (PID: Process ID).

· The **net** namespace: Managing network interfaces (NET: Networking).

· The **ipc** namespace: Managing access to IPC resources (IPC:
InterProcess Communication).

· The **mnt** namespace: Managing filesystem mount points (MNT: Mount).

· The **uts** namespace: Isolating kernel and version identifiers. (UTS:
Unix Timesharing System).

However, for user namespace you have to start remapping UIDs in Docker
Engine with the \--userns-remap flag.

[[https://docs.docker.com/get-started/overview/\#namespaces]{.ul}](https://docs.docker.com/get-started/overview/#namespaces)

[[https://success.docker.com/article/introduction-to-user-namespaces-in-docker-engine]{.ul}](https://success.docker.com/article/introduction-to-user-namespaces-in-docker-engine)

### **Answer 8: c**

*Explanation*

Docker Trusted Registry (DTR) is the enterprise-grade image storage
solution from Docker.

[[https://docs.mirantis.com/docker-enterprise/v3.0/dockeree-products/dtr.html]{.ul}](https://docs.mirantis.com/docker-enterprise/v3.0/dockeree-products/dtr.html)

### **Answer 9: b**

*Explanation*

To configure the Docker daemon to a specific logging driver, set the
value of log-driver to the name of the logging driver in the daemon.json
file.

The default logging driver is **json-file**.

To find the current default logging driver for the Docker daemon,
run docker info and search for Logging Driver. You can use the following
command on Linux, macOS, or PowerShell on Windows:

    \$ docker info \--format \'{{.LoggingDriver}}\'

[[https://docs.docker.com/config/containers/logging/configure/\#configure-the-default-logging-driver]{.ul}](https://docs.docker.com/config/containers/logging/configure/#configure-the-default-logging-driver)

### **Answer 10: a, b, c**

*Explanation*

**Docker Enterprise components**

Docker Enterprise has three major components, which together enable a
full software supply chain, from image creation, to secure image
storage, to secure image deployment.

**Docker Engine - Enterprise**: The commercially supported Docker engine
for creating images and running them in Docker containers.

**Docker Trusted Registry** (DTR): The production-grade image storage
solution from Docker.

DTR is designed to scale horizontally as your usage increases. You can
add more replicas to make DTR scale to your demand and for high
availability.

All DTR replicas run the same set of services, and changes to their
configuration are propagated automatically to other replicas.

**Universal Control Plane** (UCP): Deploys applications from images, by
managing orchestrators, like Kubernetes and Swarm.

UCP is designed for high availability (HA). You can join multiple UCP
manager nodes to the cluster, and if one manager node fails, another
takes its place automatically without impact to the cluster.

Changes to the configuration of one UCP manager node are propagated
automatically to other nodes.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 11: a**

*Explanation*

To only authenticate once, you can configure DTR to have **single
sign-on** (SSO) with UCP.

Users are shared between UCP and DTR by default, but the applications
have separate browser-based interfaces which require authentication.

When installing DTR, pass \--dtr-external-url \<url\> to enable SSO.

You can also enable single sign-on from the command line by
reconfiguring your DTR.

To do so, run the following:

    docker run \--rm -it \\

    docker/dtr:2.7.6 reconfigure \\

    \--dtr-external-url dtr.example.com \\

    ...

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 12: a**

*Explanation*

Networks used by DTR

To allow containers to communicate, when installing DTR the overlay
networks should be created.

dtr-ol this allows DTR components running on different nodes to
communicate, to replicate DTR data

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 13: a**

*Explanation*

The following logging drivers are supported.

Driver     Description

**none**   No logs are available for the container and docker logs does
not return any output.

**local**   Logs are stored in a custom format designed for minimal
overhead.

**json-file**   The logs are formatted as JSON. The default logging
driver for Docker.

**syslog**   Writes logging messages to the syslog facility. The syslog
daemon must be running on the host machine.

**journald**   Writes log messages to journald. The journald daemon must
be running on the host machine.

**gelf**     Writes log messages to a Graylog Extended Log Format (GELF)
endpoint such as Graylog or Logstash.

**fluentd**   Writes log messages to fluentd (forward input). The
fluentd daemon must be running on the host machine.

**awslogs**   Writes log messages to Amazon CloudWatch Logs.

**splunk**   Writes log messages to splunk using the HTTP Event
Collector.

**etwlogs**   Writes log messages as Event Tracing for Windows (ETW)
events. Only available on Windows platforms.

**gcplogs**   Writes log messages to Google Cloud Platform (GCP)
Logging.

**logentries**   Writes log messages to Rapid7 Logentries.

[[https://docs.docker.com/config/containers/logging/configure/\#supported-logging-drivers]{.ul}](https://docs.docker.com/config/containers/logging/configure/#supported-logging-drivers)

### **Answer 14: d**

*Explanation*

You can install Docker Engine in different ways, depending on your
needs:

· Most users set up Docker's repositories and install from them, for
ease of installation and upgrade tasks. This is the recommended
approach.

· Some users download the RPM package and install it manually and manage
upgrades completely manually. This is useful in situations such as
installing Docker on air-gapped systems with no access to the internet.

· In testing and development environments, some users choose to use
automated convenience scripts to install Docker.

[[https://docs.docker.com/engine/install/centos/\#installation-methods]{.ul}](https://docs.docker.com/engine/install/centos/#installation-methods)

### **Answer 15: d**

*Explanation*

To join a node to a swarm use the following command:

    docker swarm join \[OPTIONS\] HOST:PORT

<https://docs.docker.com/engine/reference/commandline/swarm_join/>

### **Answer 16: c**

*Explanation*

**Control groups**

Docker Engine on Linux also relies on another technology called control
groups (**cgroups**).

A cgroup limits an application to a specific set of resources. Control
groups allow Docker Engine to share available hardware resources to
containers and optionally enforce limits and constraints.

For example, you can limit the memory or CPU available to a specific
container.

[[https://docs.docker.com/get-started/overview/\#control-groups]{.ul}](https://docs.docker.com/get-started/overview/#control-groups)

### **Answer 17: b**

*Explanation*

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and
higher) use **systemd** to manage which services start when the system
boots. Ubuntu 14.10 and below use upstart.

    \$ sudo systemctl enable docker

To disable this behavior, use disable instead.

    \$ sudo systemctl disable docker

[[https://docs.docker.com/engine/install/linux-postinstall/\#configure-docker-to-start-on-boot]{.ul}](https://docs.docker.com/engine/install/linux-postinstall/#configure-docker-to-start-on-boot)

### **Answer 18: b**

*Explanation*

For high-availability you can deploy multiple DTR replicas, one on each
UCP worker node.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 19: a**

*Explanation*

To install Docker Enterprise, you will need the URL of the Docker
Enterprise repository associated with your trial or subscription:

[[https://docs.mirantis.com/docker-enterprise/v3.0/dockeree-products/docker-engine-enterprise/dee-linux/rhel.html]{.ul}](https://docs.mirantis.com/docker-enterprise/v3.0/dockeree-products/docker-engine-enterprise/dee-linux/rhel.html)

This section lists what you need to consider before installing Docker
Engine - Enterprise. Items that require action are explained below.

· Use storage driver overlay2 or devicemapper (direct-lvm mode in
production).

· Find the URL for your Docker Engine - Enterprise repo at Docker Hub.

· Uninstall old versions of Docker.

· Remove old Docker repos from /etc/yum.repos.d/.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 20: a, d**

*Explanation*

    \--cpus=\<value\>

Specify how much of the available CPU resources a container can use. For
instance, if the host machine has two CPUs and you set \--cpus=\"1.5\",
the container is guaranteed at most one and a half of the CPUs. This is
the equivalent of setting \--cpu-period=\"100000\" and
\--cpu-quota=\"150000\". Available in Docker 1.13 and higher.

    -m or \--memory=

The maximum amount of memory the container can use. If you set this
option, the minimum allowed value is 4m (4 megabyte).

Most of these options take a positive integer, followed by a suffix of
b, k, m, g, to indicate bytes, kilobytes, megabytes, or gigabytes.

[[https://docs.docker.com/config/containers/resource_constraints/]{.ul}](https://docs.docker.com/config/containers/resource_constraints/)

### **Answer 21: d**

*Explanation*

**Cache deployment strategy**

The main reason to use a DTR cache is so that users can pull images from
a service that's geographically closer to them.

In this example, a company has developers spread across three locations:
United States, Asia, and Europe. Developers working in the US office can
pull their images from DTR without problem, but developers in the Asia
and Europe offices complain that it takes them a long time to pulls
images.

To address that, you can deploy DTR caches in the Asia and Europe
offices, so that developers working from there can pull images much
faster.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/DTRcache.jpg)

### **Answer 22: b**

*Explanation*

There are a number of ways to configure the daemon flags and environment
variables for your Docker daemon. The recommended way is to use the
platform-independent daemon.json file, which is located
in /etc/docker/ on Linux by default.

[[https://docs.docker.com/config/daemon/systemd/\#custom-docker-daemon-options]{.ul}](https://docs.docker.com/config/daemon/systemd/#custom-docker-daemon-options)

### **Answer 23: b**

*Explanation*

Use docker system events to get real-time events from the server.

These events differ per Docker object type such as containers, images,
plugins, volumes and daemons.

[[https://docs.docker.com/engine/reference/commandline/system_events/]{.ul}](https://docs.docker.com/engine/reference/commandline/system_events/)

### **Answer 24: a**

*Explanation*

    \--force-new-cluster

This flag forces an existing node that was part of a quorum that was
lost to restart as a single node Manager without losing its data.

[[https://docs.docker.com/engine/reference/commandline/swarm_init/\#\--force-new-cluster]{.ul}](https://docs.docker.com/engine/reference/commandline/swarm_init/#--force-new-cluster)

### **Answer 25: b**

*Explanation*

**Troubleshoot conflicts between the daemon.json and startup scripts**

If you use a daemon.json file and also pass options to the dockerd
command manually or using start-up scripts, and these options conflict,
Docker fails to start with an error such as:

    unable to configure the Docker daemon with file /etc/docker/daemon.json:

    the following directives are specified both as a flag and in the
    configuration

    file: hosts: (from flag: \[unix:///var/run/docker.sock\], from file:
    \[tcp://127.0.0.1:2376\])

If you see an error similar to this one and you are starting the daemon
manually with flags, you may need to adjust your flags or the
daemon.json to remove the conflict.

[[https://docs.docker.com/config/daemon/\#troubleshoot-conflicts-between-the-daemonjson-and-startup-scripts]{.ul}](https://docs.docker.com/config/daemon/#troubleshoot-conflicts-between-the-daemonjson-and-startup-scripts)

### **Answer 26: c**

*Explanation*

**DTR content backed-up**

· Configurations - DTR settings and cluster configurations

· Repository metadata - Metadata such as image architecture,
repositories, images deployed, and size

· Access control to repos and images - Data about who has access to
which images and repositories

· Notary data - Signatures and digests for images that are signed

· Scan results - Information about vulnerabilities in your images

· Certificates and keys - Certificates, public keys, and private keys
that are used for mutual TLS communication

**DTR content NOT backed-up**

· Image content - The images you push to DTR. This can be stored on the
file system of the node running DTR, or other storage system, depending
on the configuration. Needs to be backed up separately, depends on DTR
configuration

· Users, orgs, teams - Create a UCP backup to back up this data

· Vulnerability database - Can be redownloaded after a restore

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 27: c**

*Explanation*

To display system-wide information use:

    docker info \[OPTIONS\]

This command displays system-wide information regarding the Docker
installation. Information displayed includes the kernel version, number
of containers and images.

https://docs.docker.com/engine/reference/commandline/info/

### **Answer 28: b**

*Explanation*

**Health checks**

DTR also exposes several endpoints you can use to assess if a DTR
replica is healthy or not:

/health: Checks if the several components of a DTR replica are healthy,
and returns a simple json response. This is useful for load balancing or
other automated health check tasks.

/load_balancer_status: Checks if the several components of a DTR replica
can be reached, and displays that information in a table. This is useful
for an administrator to gauge the status of a DTR replica.

/nginx_status: Returns the number of connections being handled by the
NGINX front-end used by DTR.

/api/v0/meta/cluster_status: Returns extensive information about all DTR
replicas.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 29: c**

*Explanation*

To create a UCP backup you should run the following command:

    \$ docker container run \\

    \--rm \\

    \--log-driver none \\

    \--name ucp \\

    \--volume /var/run/docker.sock:/var/run/docker.sock \\

    \--volume /tmp:/backup \\

    docker/ucp:3.2.6 backup \\

    \--file mybackup.tar \\

    \--passphrase \"secret12chars\" \\

    \--include-logs=false

Here, the "docker/ucp" represents a docker image, "backup" is the
command to execute.

This command should be run on a single UCP manager. This creates a tar
archive with the contents of all volumes used by UCP and streams it to
stdout. Additionally, you can include the version such as:

    docker/ucp:3.2.6 backup

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 30: d**

*Explanation*

**Docker Universal Control Plane** (UCP) is the enterprise-grade cluster
management solution from Docker.

With Docker, you can join up to thousands of physical or virtual
machines together to create a container cluster that allows you to
deploy your applications at scale. UCP extends the functionality
provided by Docker to make it easier to manage your cluster from a
centralized place.

[[https://docs.mirantis.com/docker-enterprise/v3.0/dockeree-products/ucp.html]{.ul}](https://docs.mirantis.com/docker-enterprise/v3.0/dockeree-products/ucp.html)

### **Answer 31: a, c, d**

*Explanation*

To back up Docker Enterprise, you must create individual backups for
each of the following components:

  1. Back up Docker Swarm. Back up Swarm resources like service and
network definitions.

  2. Back up Universal Control Plane (UCP). Back up UCP configurations
such as Access control, Certificates and keys, volumes = All UCP named
volumes, which include all UCP component certs and data, Monitoring data
gathered by UCP,

  3. Back up Docker Trusted Registry (DTR). Back up DTR configurations,
images, and metadata, Repository metadata, Access control to repos and
images, Notary data, Scan results.

If you do not create backups for all components, you cannot restore your
deployment to its previous state.

Role-Based Access Control (RBAC) is part of UCP.

[[https://success.docker.com/article/backup-restore-best-practices]{.ul}](https://success.docker.com/article/backup-restore-best-practices)

### **Answer 32: a, d**

*Explanation*

Docker namespaces provide a layer of isolation. Each aspect of a
container runs in a separate namespace and its access is limited to that
namespace.

Docker Engine uses namespaces such as the following on Linux:

· The **pid** namespace: Process isolation (PID: Process ID).

· The **net** namespace: Managing network interfaces (NET: Networking).

· The **ipc** namespace: Managing access to IPC resources (IPC:
InterProcess Communication).

· The **mnt** namespace: Managing filesystem mount points (MNT: Mount).

· The **uts** namespace: Isolating kernel and version identifiers. (UTS:
Unix Timesharing System).

[[https://docs.docker.com/get-started/overview/\#namespaces]{.ul}](https://docs.docker.com/get-started/overview/#namespaces)

### **Answer 33: a, c, d**

*Explanation*

You can install DTR on-premises or on a cloud provider. To install DTR,
all nodes must:

· Be a worker node managed by UCP (Universal Control Plane). DTR
replicas are installed one on each UCP worker node.

· Have a fixed hostname.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 34: b**

*Explanation*

You can use the https://\<ucp-manager-url\>/\_ping endpoint to check the
health of a single UCP manager node.

When you access this endpoint, the UCP manager validates that all its
internal components are working, and returns one of the following HTTP
error codes:

· 200, if all components are healthy

· 500, if one or more components are not healthy

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 35: b**

*Explanation*

The Docker Engine joins the swarm depending on the join-token you
provide to the docker swarm join command.

To retrieve the join command including the join token for worker nodes,
run the following command on a **manager node**:

    \$ docker swarm join-token worker

To add a worker to this swarm, run the following command with the output
from the previous command:

        docker swarm join \\

        \--token
    SWMTKN-1-49nj1cmql0jkz5s954yi3oex3nedyz0fb0xx14ie39trti4wxv-8vxv8rssmk743ojnwacrr2e7c
    \\

        192.168.99.100:2377

This node joined a swarm as a worker.

[[https://docs.docker.com/engine/swarm/join-nodes/\#join-as-a-worker-node]{.ul}](https://docs.docker.com/engine/swarm/join-nodes/#join-as-a-worker-node)

### **Answer 36: a**

*Explanation*

There are a number of ways to configure the daemon flags and environment
variables for your Docker daemon. The recommended way is to use the
platform-independent daemon.json

[[https://docs.docker.com/config/daemon/systemd/\#custom-docker-daemon-options]{.ul}](https://docs.docker.com/config/daemon/systemd/#custom-docker-daemon-options)

### **Answer 37: a, b, d**

*Explanation*

Docker Engine combines the namespaces, control groups, and UnionFS into
a wrapper called a **container format**. The default container format is
libcontainer.

In the future, Docker may support other container formats by integrating
with technologies such as BSD Jails or Solaris Zones.

[[https://docs.docker.com/get-started/overview/\#container-format]{.ul}](https://docs.docker.com/get-started/overview/#container-format)

### **Answer 38: c**

*Explanation*

UCP always runs with HTTPS enabled. When you connect to UCP, you need to
make sure that the hostname that you use to connect is recognized
by **UCP's certificates**.

If, for instance, you put UCP behind a load balancer that forwards its
traffic to your UCP instance, your requests will be for the load
balancer's hostname or IP address, not UCP's. UCP will reject these
requests unless you include the load balancer's address as a **Subject
Alternative Name** (or SAN) in UCP's certificates.

If you use your own TLS certificates, make sure that they have the
correct SAN values

If you want to use the self-signed certificate that UCP has out of the
box, you can set up the SANs when you install UCP with
the \--san argument. You can also add them after installation.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 39: b**

*Explanation*

Docker includes multiple logging mechanisms to help you get information
from running containers and services. These mechanisms are
called **logging drivers**.

To find the current logging driver for a running container, run the
docker inspect command, substituting the container name or ID for
\<CONTAINER\>:

    \$ docker inspect \<CONTAINER\>

[[https://docs.docker.com]{.ul}](https://docs.docker.com/config/containers/logging/configure/)/config/containers/logging/configure/

### **Answer 40: b, c**

*Explanation*

Docker provides two modes for delivering messages from the container to
the log driver:

· (default) direct, blocking delivery from container to driver

· non-blocking delivery that stores log messages in an intermediate
per-container ring buffer for consumption by driver

[[https://docs.docker.com/config/containers/logging/configure/\#configure-the-delivery-mode-of-log-messages-from-container-to-log-driver]{.ul}](https://docs.docker.com/config/containers/logging/configure/#configure-the-delivery-mode-of-log-messages-from-container-to-log-driver)

### **Answer 41: c**

*Explanation*

To make the modifications and send the HUP signal in one-line use:

echo \'{\"debug\": true}\' \> **/etc/docker**/daemon.json ; sudo kill
-HUP

[[https://docs.docker.com/config/daemon/\#enable-debugging]{.ul}](https://docs.docker.com/config/daemon/#enable-debugging)

### **Answer 42: c**

*Explanation*

Each Docker daemon has a default logging driver, which each container
uses unless you configure it to use a different logging driver.

To configure the Docker daemon to default to a specific logging driver,
set the value of **log-driver** to the name of the logging driver in the
daemon.json file, which is located in /etc/docker/ on Linux hosts or
C:\\ProgramData\\docker\\config\\ on Windows server hosts.

<https://docs.docker.com/config/containers/logging/configure/>

### **Answer 43: c**

*Explanation*

By default, each container's access to the host machine's CPU cycles is
unlimited. You can set various constraints to limit a given container's
access to the host machine's CPU cycles.

Several runtime flags allow you to configure the amount of access to CPU
resources your container has. When you use these settings, Docker
modifies the settings for the container's cgroup on the host machine.

    \--cpuset-cpus

Limit the specific CPUs or cores a container can use. A comma-separated
list or hyphen-separated range of CPUs a container can use, if you have
more than one CPU. The first CPU is numbered 0. A valid value might be
0-3 (to use the first, second, third, and fourth CPU) or 1,3 (to use the
second and fourth CPU).

[[https://docs.docker.com/config/containers/resource_constraints/\#cpu]{.ul}](https://docs.docker.com/config/containers/resource_constraints/#cpu)

We can set cpus in which to allow execution for containers.

Examples:

    \$ docker run -it \--cpuset-cpus=\"1,3\" ubuntu:14.04 /bin/bash

This means processes in container can be executed on cpu 1 and cpu 3.

    \$ docker run -it \--cpuset-cpus=\"0-2\" ubuntu:14.04 /bin/bash

This means processes in container can be executed on cpu 0, cpu 1 and
cpu 2.

[[https://docs.docker.com/engine/reference/run/\#cpuset-constraint]{.ul}](https://docs.docker.com/engine/reference/run/#cpuset-constraint)

### **Answer 44: b, d**

*Explanation*

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and
higher) use **systemd** to manage which services start when the system
boots. Ubuntu 14.10 and below use upstart.

    \$ sudo systemctl enable docker

To disable this behavior, use disable instead.

    \$ sudo systemctl disable docker

[[https://docs.docker.com/engine/install/linux-postinstall/\#configure-docker-to-start-on-boot]{.ul}](https://docs.docker.com/engine/install/linux-postinstall/#configure-docker-to-start-on-boot)

### **Answer 45: a**

*Explanation*

**Control groups**

Docker Engine on Linux also relies on another technology called control
groups (**cgroups**).

A cgroup limits an application to a specific set of resources. Control
groups allow Docker Engine to share available hardware resources to
containers and optionally enforce limits and constraints.

For example, you can limit the memory or CPU available to a specific
container.

[[https://docs.docker.com/get-started/overview/\#control-groups]{.ul}](https://docs.docker.com/get-started/overview/#control-groups)

### **Answer 46: c**

*Explanation*

Backups contain UCP configuration metadata to re-create configurations
such as Administration Settings values such as LDAP and SAML, and RBAC
configurations (Collections, Grants, Roles, User, and more):

The following example shows how to create a UCP backup on a manager
node, encrypt it by using a passphrase, decrypt it, verify its contents,
and store it locally on the node at /tmp/mybackup.tar:

    \$ docker container run \\

    \--rm \\

    \--log-driver none \\

    \--name ucp \\

    \--volume /var/run/docker.sock:/var/run/docker.sock \\

    \--volume /tmp:/backup \\

    docker/ucp:3.2.6 backup \\

    \--file mybackup.tar \\

    \--passphrase \"secret12chars\" \\

    \--include-logs=false

Here, the "docker/ucp" represents a docker image, "backup" is the
command to execute.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 47: c**

*Explanation*

There are two ways to enable debugging. The recommended approach is to
set the debug key to true in the daemon.json file. This method works for
every Docker platform.

Find the daemon.json file, which is usually located in /etc/docker/. You
may need to create this file, if it does not yet exist.

If the file is empty, add the following:

    {

      \"debug\": true

    }

After the daemon.json file is modified, you should send a HUP signal to
the daemon to cause it to reload its configuration. On Linux hosts, use
the following command.

sudo kill -SIGHUP \$(pidof dockerd)

Instead of following this procedure, you can also stop the Docker daemon
and restart it manually with the debug flag -D. However, this may result
in Docker restarting with a different environment than the one the
hosts' startup scripts create, and this may make debugging more
difficult.

[[https://docs.docker.com/config/daemon/\#enable-debugging]{.ul}](https://docs.docker.com/config/daemon/#enable-debugging)

### **Answer 48: c**

*Explanation*

**Start the daemon manually**

If you don't want to use a system utility to manage the Docker daemon,
or just want to test things out, you can manually run it using the
dockerd command. You may need to use sudo, depending on your operating
system configuration.

When you start Docker this way, it runs in the foreground and sends its
logs directly to your terminal.

    \$ dockerd

    INFO\[0000\] +job init_networkdriver()

    INFO\[0000\] +job serveapi(unix:///var/run/docker.sock)

    INFO\[0000\] Listening for HTTP on unix (/var/run/docker.sock)

To stop Docker when you have started it manually, issue a Ctrl+C in your
terminal.

[[http://dockerlabs.collabnix.com/beginners/components/daemon/]{.ul}](http://dockerlabs.collabnix.com/beginners/components/daemon/)

### **Answer 49: d**

*Explanation*

**Health checks**

DTR also exposes several endpoints you can use to assess if a DTR
replica is healthy or not:

/health: Checks if the several components of a DTR replica are healthy,
and returns a simple json response. This is useful for load balancing or
other automated health check tasks.

/load_balancer_status: Checks if the several components of a DTR replica
can be reached, and displays that information in a table. This is useful
for an administrator to gauge the status of a DTR replica.

/nginx_status: Returns the number of connections being handled by the
NGINX front-end used by DTR.

/api/v0/meta/cluster_status: Returns extensive information about all DTR
replicas.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)
