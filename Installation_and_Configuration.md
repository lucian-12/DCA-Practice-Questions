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
