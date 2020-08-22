### **Answer 1: b**

*Explanation*

The manager node also generates two tokens to use when you join
additional nodes to the swarm: one worker token and one manager token.
Each token includes the digest of the root CA's certificate and a
randomly generated secret. When a node joins the swarm, the joining node
uses the digest to validate the root CA certificate from the remote
manager. The remote manager uses the secret to ensure the joining node
is an approved node.

Each time a new node joins the swarm, the manager issues a certificate
to the node. The certificate contains a randomly generated node ID to
identify the node under the certificate common name (CN) and the role
under the organizational unit (OU). The node ID serves as the
cryptographically secure node identity for the lifetime of the node in
the current swarm.

The diagram below illustrates how manager nodes and worker nodes encrypt
communications using a minimum of TLS 1.2.

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/dockerTLS.png)

[[https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/]{.ul}](https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/)

### **Answer 2: c**

*Explanation*

When communicating over an untrusted medium such as the internet, it is
critical to ensure the integrity and the publisher of all the data a
system operates on. You use the Docker Engine to push and pull images
(data) to a public or private registry. Content trust gives you the
ability to verify both the integrity and the publisher of all the data
received from a registry over any channel.

**Docker Content Trust** (DCT) provides the ability to use digital
signatures for data sent to and received from remote Docker registries.
These signatures allow client-side or runtime verification of the
integrity and publisher of specific image tags.

[[https://docs.docker.com/engine/security/trust/content_trust/\#about-docker-content-trust-dct]{.ul}](https://docs.docker.com/engine/security/trust/content_trust/#about-docker-content-trust-dct)

### **Answer 3: a**

*Explanation*

Subjects are individual users or teams within an organization. Teams are
typically **backed by an LDAP/AD group** or search filter. It is also
possible to **add users manually**. But it is not possible to have a
hybrid composition of users. In other words, the list of users within a
team should be derived from a directory server (e.g. AD) or should be
added manually, not both.

[[https://success.docker.com/article/docker-enterprise-best-practices]{.ul}](https://success.docker.com/article/docker-enterprise-best-practices)

### **Answer 4: c**

*Explanation*

**Subjects**

A subject represents a user, team, or organization. A subject is granted
a role for a collection of resources. These groups of users are the same
across UCP and DTR making RBAC management across the entire software
pipeline uniform.

**User** - A single user or system account that an authentication
backend (AD/LDAP) has validated.

**Team** - A group of users that share a set of permissions defined in
the team itself. A team exists only as part of an organization, and all
team members are members of the organization. A team can exist in one
organization only. Assign users to one or more teams and one or more
organizations.

**Organization** - The largest organizational unit in Docker Enterprise.
Organizations group together teams to provide broader scope to apply
access policy against.

[[https://success.docker.com/article/security-best-practices\#dtrsecurity]{.ul}](https://success.docker.com/article/security-best-practices#dtrsecurity)

### **Answer 5: c**

*Explanation*

UCP has **role-based access control** (RBAC), so that you can control
who can access and make changes to your cluster and applications.

Using the UI for Docker Enterprise of Docker Universal Control Plane
(UCP), you authorize users to view, edit, and use cluster resources by
granting role-based permissions against resource sets.

To authorize access to cluster resources across your organization, UCP
administrators might take the following high-level steps:

· Add and configure subjects (users, teams, and service accounts).

· Define custom roles (or use defaults) by adding permitted operations
per type of resource.

· Group cluster resources into resource sets of Swarm collections or
Kubernetes namespaces.

· Create grants by combining subject + role + resource set.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 6: c**

*Explanation*

**Rotating the CA certificate**

In the event that a cluster CA key or a manager node is compromised, you
can rotate the swarm root CA so that none of the nodes trust
certificates signed by the old root CA anymore.

Run docker swarm ca \--rotate to generate a new CA certificate and key.
If you prefer, you can pass the \--ca-cert and \--external-ca flags to
specify the root certificate and to use a root CA external to the swarm.
Alternately, you can pass the \--ca-cert and \--ca-key flags to specify
the exact certificate and key you would like the swarm to use.

[[https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/]{.ul}](https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/)

### **Answer 7: a**

*Explanation*

Having a central location for all Engine and container logs is
recommended. This provides \"off-node\" access to all the logs,
empowering developers without having to grant them SSH access.

To enable centralized logging, modify /etc/docker/daemon.json and add
the following:

    {

      \"log-level\": \"syslog\",

      \"log-opts\": {syslog-address=tcp://192.x.x.x}

    }

Then restart the daemon:

    sudo systemctl restart docker

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 8: d**

*Explanation*

From the Components view, the CVE number, a link to CVE database, file
path, layers affected, severity, and description of severity are
available.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 9: c**

*Explanation*

Collections

Docker Enterprise enables controlling access to swarm resources by
using **collections**. A collection is a grouping of swarm cluster
resources that you access by specifying a directory-like path. Before
grants can be implemented, collections need to be designed to group
resources in a way that makes sense for an organization.

The following example shows the potential access policy of an
organization. Consider an organization with two application teams,
Mobile and Payments, that share cluster hardware resources, but still
need to segregate access to the applications. Collections should be
designed to map to the organizational structure desired, in this case
the two application teams.

### **Answer 10: a**

*Explanation*

Docker 1.13 introduces the ability to protect the mutual TLS encryption
key and the key used to encrypt and decrypt secrets, by allowing you to
take ownership of these keys and to require manual unlocking of your
managers. This feature is called **autolock**.

When Docker restarts, you must unlock the swarm first, using a key
encryption key generated by Docker when the swarm was locked. You can
rotate this key encryption key at any time.

To enable autolock on an existing swarm, set the autolock flag to true.

    docker swarm update \--autolock=true

[[https://docs.docker.com/engine/swarm/swarm_manager_locking/\#enable-or-disable-autolock-on-an-existing-swarm]{.ul}](https://docs.docker.com/engine/swarm/swarm_manager_locking/#enable-or-disable-autolock-on-an-existing-swarm)

Collections are implemented in UCP through the use of **Docker labels**.
All resources within a given collection are labeled with the collection,
/production/mobile for instance.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 11: b**

*Explanation*

Only users with write access to a repository can manually start a scan.
Users with **read-only **access can view the scan results, but cannot
start a new scan.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 12: b**

*Explanation*

As of Docker Engine 18.06 there is a docker trust command that will
streamline the image signing process. The old is Notary. Notary is a
tool for publishing and managing trusted collections of content.
Publishers can digitally sign collections and consumers can verify
integrity and origin of content. This ability is built on a
straightforward key management and signing interface to create signed
collections and configure trusted publishers.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices#defenseinformationsystemsagency(disa)securitytechnicalimplementationguides(stig))

### **Answer 13: d**

*Explanation*

**Secret:**

In terms of Docker Swarm services, a secret is a blob of data, such as a
password, SSH private key, SSL certificate, or another piece of data
that should **not** be transmitted over a network or stored unencrypted
in a Dockerfile or in your application's source code.

[[https://docs.docker.com/engine/swarm/secrets/\#about-secrets]{.ul}](https://docs.docker.com/engine/swarm/secrets/#about-secrets)

The command to create a secret from a file or standard input (STDIN) as
content is:

    docker secret create \[OPTIONS\] SECRET \[file\|-\]

Since this is a cluster management command, it must be executed on
a **swarm manager node**.

[[https://docs.docker.com/engine/reference/commandline/secret_create/]{.ul}](https://docs.docker.com/engine/reference/commandline/secret_create/)

Note: After you create a secret, you cannot update it. You can only
remove and re-create it, and you cannot remove a secret that a service
is using.

[[https://docs.docker.com/engine/swarm/secrets/\#advanced-example-use-secrets-with-a-wordpress-service]{.ul}](https://docs.docker.com/engine/swarm/secrets/#advanced-example-use-secrets-with-a-wordpress-service)

Secrets are encrypted during transit and at rest in a Docker swarm (The
secret is stored in the Raft log, which is encrypted)

### **Answer 14: c**

*Explanation*

You don't need to run the docker client with sudo or the docker group
when you use **certificate authentication**. That means anyone with the
keys can give any instructions to your Docker daemon, giving them root
access to the machine hosting the daemon. However, guard these keys as
you would a root password!

<https://docs.docker.com/engine/security/https/>

### **Answer 15: a**

*Explanation*

Docker UCP integrates with LDAP directory services, so that you can
manage users and groups from your organization's directory and it will
automatically propagate that information to UCP and DTR.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 16: c**

*Explanation*

**Docker Content Trust** (DCT) provides the ability to use digital
signatures for data sent to and received from remote Docker registries.
These signatures allow client-side or runtime verification of the
integrity and publisher of specific image tags.

[[https://docs.docker.com/engine/security/trust/content_trust/\#about-docker-content-trust-dct]{.ul}](https://docs.docker.com/engine/security/trust/content_trust/#about-docker-content-trust-dct)

### **Answer 17. b**

*Explanation*

Sensitive information to containers running on a Swarm are normally
stored in a secret.

A **secret** (usually containing credentials, certificates, and other
private information) is provided to service at runtime. The secret is
saved in the Raft logs.

The Raft logs used by swarm managers are encrypted on disk by default.

When Docker restarts, both the TLS key used to encrypt communication
among swarm nodes, and the key used to **encrypt and decrypt Raft
logs** on disk, are loaded into each manager node's memory.

Docker 1.13 introduces the ability to protect the mutual TLS encryption
key and the key used to encrypt and decrypt Raft logs at rest, by
allowing you to take ownership of these keys and to require manual
unlocking of your managers. This feature is called **autolock**.

When Docker restarts, you must unlock the swarm first, using a key
encryption key generated by Docker when the swarm was locked. You can
rotate this key encryption key at any time.

When you initialize a new swarm, you can use the \--autolock flag to
enable autolocking of swarm manager nodes when Docker restarts.

    docker swarm init \--autolock

To enable autolock on an existing swarm, set the autolock flag to true.

    docker swarm update \--autolock=true

[[https://docs.docker.com/engine/swarm/swarm_manager_locking/]{.ul}](https://docs.docker.com/engine/swarm/swarm_manager_locking/)

[[https://medium.com/lucjuggery/raft-logs-on-swarm-mode-1351eff1e690]{.ul}](https://medium.com/lucjuggery/raft-logs-on-swarm-mode-1351eff1e690)

### **Answer 18: b**

*Explanation*

A client bundle contains a private and public key pair that authorizes
your requests in UCP. In order to authenticate your requests, you can
download client certificate bundle to your local computer.

UCP issues different types of certificates depending on the user:

· **User certificate bundles**: only allow running docker commands
through a UCP manager node.

· **Admin user certificate bundles**: allow running docker commands on
the Docker Engine of any node.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 19: a**

*Explanation*

When you create a swarm by running docker swarm init, Docker designates
itself as a manager node. By default, the manager node generates a new
root Certificate Authority (CA) along with a key pair, which are used to
secure communications with other nodes that join the swarm.

If you prefer, you can specify your own externally-generated root CA,
using the \--external-ca flag of the docker swarm init command.

[[https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/]{.ul}](https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/)

### **Answer 20: a**

*Explanation*

You can create by combining **subject** + **role** + **resource** set.

A grant defines who has how much access to what resources. Each grant is
a 1:1:1 mapping of subject, role, and resource set.

For example, you can grant the "Prod Team" "Restricted Control" over
services in the "/Production" collection.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 21: a**

*Explanation*

Secret:

In terms of Docker Swarm services, a secret is a blob of data, such as a
password, SSH private key, SSL certificate, or another piece of data
that should not be transmitted over a network or stored unencrypted in a
Dockerfile or in your application's source code.

[[https://docs.docker.com/engine/swarm/secrets/\#about-secrets]{.ul}](https://docs.docker.com/engine/swarm/secrets/#about-secrets)

Note: After you create a secret, you cannot update it. You can only
remove and re-create it, and you cannot remove a secret that a service
is using.

[[https://docs.docker.com/engine/swarm/secrets/\#advanced-example-use-secrets-with-a-wordpress-service]{.ul}](https://docs.docker.com/engine/swarm/secrets/#advanced-example-use-secrets-with-a-wordpress-service)

Add or remove secrets

Use the \--secret-add or \--secret-rm options add or remove a service's
secrets.

For example:

    docker service update \\

         \--secret-rm mysql_password \\

         \--secret-add
    source=mysql_password_v2,target=wp_db_password,mode=0400 \\

         wordpress  

This triggers a rolling restart of the WordPress service and the new
secret is used.

The following example adds a secret named ssh-2 and removes ssh-1:

    \$ docker service update \\

        \--secret-add source=ssh-2,target=ssh-2 \\

        \--secret-rm ssh-1 \\

        Myservice

[[https://docs.docker.com/engine/reference/commandline/service_update/\#add-or-remove-secrets]{.ul}](https://docs.docker.com/engine/reference/commandline/service_update/#add-or-remove-secrets)

### **Answer 22: a, b, c, d**

*Explanation*

By default, Docker runs through a non-networked UNIX socket.

It can also optionally communicate using an HTTP socket. If you need
Docker to be reachable through the network in a safe manner, you can
enable TLS by specifying the tlsverify flag and pointing Docker's
tlscacert flag to a trusted CA certificate.

TLS must be enabled in order to have the **Docker client** and
the **daemon** communicate securely over HTTPS.

Additionally, TLS ensures authenticity of the registry endpoint and that
traffic to/from registry is encrypted.

To ensure the traffic between the Docker registry server and the Docker
daemon (a client of the registry server) is encrypted and properly
authenticated use certificate-based client-server authentication.

[[https://docs.docker.com/engine/security/certificates/]{.ul}](https://docs.docker.com/engine/security/certificates/)

In the **daemon mode**, it only allows connections from clients
authenticated by a certificate signed by that CA.

In the client mode, it only connects to servers with a certificate
signed by that CA.

[[https://docs.docker.com/engine/security/https/]{.ul}](https://docs.docker.com/engine/security/https/)

**Docker Content Trust** (DCT) provides the ability to use digital
signatures for data sent to and received from remote Docker registries.
These signatures allow client-side or runtime verification of the
integrity and publisher of specific image tags.

[[https://docs.docker.com/engine/security/trust/content_trust/\#about-docker-content-trust-dct]{.ul}](https://docs.docker.com/engine/security/trust/content_trust/#about-docker-content-trust-dct)

Docker Content Trust Signature Verification

The Docker Engine can be configured to only run signed images. The
Docker Content Trust signature verification feature is built directly
into the dockerd binary.

This is configured in the Dockerd configuration file.

To enable this feature, trustpinning can be configured in daemon.json,
whereby only repositories signed with a user-specified root key can be
pulled and run.

[[https://docs.docker.com/engine/security/security/\#docker-content-trust-signature-verification]{.ul}](https://docs.docker.com/engine/security/security/#docker-content-trust-signature-verification)

**Secure computing mode** (seccomp) is a Linux kernel feature. You can
use it to restrict the actions available within the container. The
seccomp() system call operates on the seccomp state of the calling
process. You can use this feature to restrict your application's access.

[[https://docs.docker.com/engine/security/seccomp/]{.ul}](https://docs.docker.com/engine/security/seccomp/)

### **Answer 23: c**

*Explanation*

**Team's permissions**

Permissions are cumulative. For example, if you have Write permissions,
you automatically have Read permissions:

· **Read** access allows users to view, search, and pull a private
repository in the same way as they can a public repository.

· **Write** access allows users to push to repositories on Docker Hub.

· **Admin** access allows users to modify the repositories
"Description", "Collaborators" rights, "Public/Private" visibility, and
"Delete".

[[https://docs.docker.com/docker-hub/orgs/\#permissions-reference]{.ul}](https://docs.docker.com/docker-hub/orgs/#permissions-reference)

### **Answer 24: b**

*Explanation*

**Image Immutability**

As of DTR 2.3.0, there is an option to set a repository to Immutable.
Setting a repository to Immutable means the tags can not be overwritten.
This is a great feature for ensure the base images do not change over
time. This next example is of the Alpine base image. Ideally CI would
update the base image and push to DTR with a specific tag. Being
Immutable simply guarantees that an authorized user can always go back
to the specific tag and trust it has not changed. An Image Promotion
Policy can extend on this.

https://success.docker.com/article/security-best-practices

### **Answer 25: a**

*Explanation*

**Limit Root Access to Node**

Docker Enterprise uses a completely separate authentication backend from
the host, providing a clear separation of duties. Docker Enterprise can
leverage an existing LDAP/AD infrastructure for authentication. It even
utilizes RBAC Labels to control access to objects like images and
running containers, meaning teams of users can be given full access to
running containers. With this access, users can watch the logs and
execute a shell inside the running container without needing to ever log
into the host. Limiting the number of users that have access to the host
reduces the attack surface.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 26: a, d, e**

*Explanation*

**Secrets**

A Docker secret is a blob of sensitive data that should not be
transmitted over a network, such as:

· Usernames and passwords

· TLS certificates and keys

· SSH keys

· Other important data such as the name of a database or internal server

· Generic strings or binary content (up to 500 kb in size)

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 27: b**

*Explanation*

To use the Docker CLI with UCP, download a client certificate
bundle(zip) by using the UCP web UI.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 28: a**

*Explanation*

Control Plane Security

Docker Swarm comes with integrated PKI. All managers and nodes in the
Swarm have a **cryptographically signed identity** in the form of
a **signed certificate**. All manager-to-manager and manager-to-node
control communication is secured out of the box with TLS. There is no
need to generate certs externally or set up any CAs manually to get
end-to-end control plane traffic secured in Docker Swarm mode.
Certificates are periodically and automatically rotated.

[[https://success.docker.com/article/networking\#dockernetworksecurityandencryption]{.ul}](https://success.docker.com/article/networking#dockernetworksecurityandencryption)

### **Answer 29: d**

*Explanation*

Linux capabilities are an even more granular way of reducing surface
area. Docker Engine has a default list of capabilities that are kept for
newly-created containers, and by using the \--cap-drop option for docker
run, users can exclude additional capabilities from being used by
processes inside the container on a capability-by-capability basis. All
privileges can be dropped with the \--user option.

Likewise, capabilities that are, by default, not granted to new
containers can be added with the \--cap-add option. This is discouraged
unless absolutely necessary, and using \--cap-add=ALL is highly
discouraged.

Limiting the capabilities of a container reduces the attack surface.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

[[https://docs.docker.com/engine/reference/run/\#runtime-privilege-and-linux-capabilities]{.ul}](https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities)

### **Answer 30: a**

*Explanation*

The default roles in UCP are **None**, **View Only**, **Restricted
Control**, **Scheduler**, and **Full Control**.

Each of these roles have a set of operations that define the permissions
associated with the role. Additional custom roles can be defined by
combining a unique set of permissions. Custom roles can be leveraged to
accommodate fine-grained access control as required for certain
organizations and security controls.

[[https://success.docker.com/article/docker-enterprise-best-practices]{.ul}](https://success.docker.com/article/docker-enterprise-best-practices)

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 31: c**

*Explanation*

Collections are groupings of objects within UCP. A collection can be
made up of one or many of nodes, stacks, containers, services, volumes,
networks, secrets, or configs --- or it can hold other collections.

To associate a node or a stack or any resource with a collection, that
resource should share the label com.docker.ucp.access.label with the
collection.

A resource can be associated with zero or multiple collections, and a
collection can have zero or multiple resources or other child
collections in it. Collections within collections allow the structuring
of resource objects in a hierarchical nature and can significantly
simplify access control. Access provided at a top level collection is
inherited by all its children, including any child collections.

https://success.docker.com/article/docker-enterprise-best-practices

### **Answer 32: d**

*Explanation*

Image scan is a feature of **Docker trusted Repository** DTR, which is
part of Docker Entreprise Edition.

To use the image scanning feature, make sure that you or your
organization has purchased a DTR license that includes Docker Security
Scanning, and that your Docker ID can access and download this license
from the Docker Hub.

After you get the license, you'll need to Enable DTR security scanning.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 33: a**

*Explanation*

By default, Docker containers are "unprivileged" and cannot, for
example, run a Docker daemon inside a Docker container. This is because
by default a container is not allowed to access any devices, but a
"privileged" container is given access to all devices (see the
documentation on cgroups devices).

When the operator executes docker run \--privileged, Docker will enable
access to all devices on the host as well as set some configuration in
AppArmor or SELinux to allow the container nearly all the same access to
the host as processes running outside containers on the host. Additional
information about running with \--privileged is available on the Docker
Blog.

If you want to limit access to a specific device or devices you can use
the \--device flag. It allows you to specify one or more devices that
will be accessible within the container.

    \$ docker run \--device=/dev/snd:/dev/snd \...

Following the least privileged principle, you should use \--device
instead of \--priviledged.

[[https://docs.docker.com/engine/reference/run/\#/runtime-privilege-and-linux-capabilities]{.ul}](https://docs.docker.com/engine/reference/run/#/runtime-privilege-and-linux-capabilities)

Docker Engine has a default list of capabilities for all newly created
containers.

### **Answer 34: b, c, d**

*Explanation*

The swarm mode **public key infrastructure** (PKI) system built into
Docker makes it simple to securely deploy a container orchestration
system. The nodes in a swarm use **mutual Transport Layer
Security** (TLS) to authenticate, authorize, and encrypt the
communications with other nodes in the swarm.

[[https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/]{.ul}](https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/)

### **Answer 35: a, c, d**

*Explanation*

**Garbage Collection**

Garbage collection is an often-overlooked area from a security
standpoint. Old, out-of-date images may contain security flaws or
exploitable vulnerabilities; removing unnecessary images is important.
Garbage collection is a feature that ensures that unreferenced images
(and layers) are removed.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 36: c**

*Explanation*

**Seccomp** (short for Secure Computing Mode) is a security feature of
the Linux kernel, used to restrict the syscalls available to a given
process. This facility has been in the kernel in various forms since
2.6.12 and has been available in Docker Engine since 1.10. The current
implementation in Docker Engine provides a default set of restricted
syscalls and also allows syscalls to be filtered via either a whitelist
or a blacklist on a per-container basis (i.e. different filters can be
applied to different containers running in the same Engine). Seccomp
profiles are applied at container creation time and cannot be altered
for running containers.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 37: c**

*Explanation*

When you deploy UCP, it starts running a globally scheduled service
called **ucp-agent**. This service monitors the node where it's running
and starts and stops UCP services, based on whether the node is a
manager or a worker node.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 38: b**

*Explanation*

When you are running a docker command, Docker attempts to verify that
the certificate in use is signed by UCP\'s certificate authority and
that the domain name or IP used to connect to UCP is listed as a subject
alternative name (SAN) in the UCP certificate.

If you see the following error "x509: certificate signed by unknown
authority", then Docker has not been provided with the ca certificate.
To resolve this issue, use a UCP client bundle to connect to UCP from
the CLI.

[[https://success.docker.com/article/docker-login-to-dtr-fails-with-x509-certificate-error]{.ul}](https://success.docker.com/article/docker-login-to-dtr-fails-with-x509-certificate-error)

### **Answer 39: b**

*Explanation*

A **client bundle** contains a private and public key pair that
authorizes your requests in UCP.

Using client certificate bundle on your local computer, you can use it
to authenticate your requests.

What is a client bundle?

A client bundle is a group of certificates downloadable directly from
the Docker Universal Control Plane (UCP) user interface within the admin
section for "My Profile".

This allows you to authorize a remote Docker engine to a specific user
account managed in Docker EE, absorbing all associated RBAC controls in
the process. You can now execute docker swarm commands from your remote
machine that take effect on the remote cluster.

[[https://www.docker.com/blog/get-familiar-docker-enterprise-edition-client-bundles/]{.ul}](https://www.docker.com/blog/get-familiar-docker-enterprise-edition-client-bundles/)

### **Answer 40: a, c**

*Explanation*

Docker 1.13 introduces the ability to protect the mutual TLS encryption
key and the key used to encrypt and decrypt secrets, by allowing you to
take ownership of these keys and to require manual unlocking of your
managers. This feature is called **autolock**.

When Docker restarts, you must unlock the swarm first, using a key
encryption key generated by Docker when the swarm was locked. You can
rotate this key encryption key at any time.

To enable autolock on an existing swarm, set the autolock flag to true.

    docker swarm update \--autolock=true

[[https://docs.docker.com/engine/swarm/swarm_manager_locking/\#enable-or-disable-autolock-on-an-existing-swarm]{.ul}](https://docs.docker.com/engine/swarm/swarm_manager_locking/#enable-or-disable-autolock-on-an-existing-swarm)

### **Answer 41: b**

*Explanation*

If the vulnerability is in a base layer (such as an operating system)
you might not be able to correct the issue in the image, since when one
base layer needs to be rebuilt, all subsequent layers also need to be
rebuilt.

In this case, you might switch to a different version of the base layer,
or you might find an equivalent, less vulnerable base layer. You might
also decide that the vulnerability or exposure is acceptable.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 42: b**

*Explanation*

While it's highly recommended to secure your registry using a TLS
certificate issued by a known CA, you can choose to use self-signed
certificates, or use your registry over an unencrypted HTTP connection.
Either of these choices involves security trade-offs and additional
configuration steps.

This procedure configures Docker to entirely disregard security for your
registry.

1\. Edit the daemon.json file, whose default location is
/etc/docker/daemon.json. Add the following content.

    {

      \"insecure-registries\": \[\"myregistrydomain.com:5000\"\]

    }

2\. Restart Docker for the changes to take effect.

3\. Repeat these steps on every Engine host that wants to access your
registry.

Alternatively, you can pass the \--engine-insecure-registry flag when
the docker engine is started.

[[https://docs.docker.com/registry/insecure/]{.ul}](https://docs.docker.com/registry/insecure/)

### **Answer 43: d**

*Explanation*

Container UID Management

By default the user inside the container is root. Using a defense in
depth model, it is recommended that not all containers run as root. An
easy way to mitigate this is to use the \--user declaration at run time.
The container runs as the specified user, essentially removing root
access.

Developers should use root as little as possible inside the container.
Developers should create their app containers with the USER declaration
in their Dockerfiles.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

[[https://docs.docker.com/engine/reference/builder/\#user]{.ul}](https://docs.docker.com/engine/reference/builder/#user)

### **Answer 44: b**

*Explanation*

UCP services include a component called **ucp-auth-api**, which is the
centralized service for identity and authentication used by UCP and DTR.

All UCP services are exposed using **HTTPS**, to ensure all
communications between clients and UCP are **encrypted**.

By default, this is done using self-signed TLS certificates that are not
trusted by client tools like web browsers. So when you try to access
UCP, your browser warns that it doesn't trust UCP or that UCP has an
invalid certificate. The same happens with other client tools.

You can configure UCP to use your own TLS certificates, so that it is
automatically trusted by your browser and client tools.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 45: b**

*Explanation*

Using external certificates is recommended when integrating with a
corporate environment. Using external, officially-signed certificates
simplifies having to distribute internal Certificate Authority (CA)
certificates. One best practice is to use the Certificate Authority for
your organization. Reduce the number of certificates by adding
multiple **Subject Alternative Names** (SANs) to a single certificate.
This allows the certificate to be valid for multiple URLs. For example,
you can set up a certificate for ucp.example.com, dtr.example.com, and
all the underlying hostnames and IP addresses. One certificate/key pair
makes deploying certs easier.

[[https://success.docker.com/article/security-best-practices\#dtrsecurity]{.ul}](https://success.docker.com/article/security-best-practices#dtrsecurity)

### **Answer 46: a**

*Explanation*

**Docker Trusted Registry** can scan images in your repositories to
verify that they are free from known security vulnerabilities or
exposures, using Docker Security Scanning.

Docker Security Scanning is available as an add-on to Docker Trusted
Registry, and an administrator configures it for your DTR instance.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 47: b**

*Explanation*

**Node Certificate Expiration**

Universal Control Plane\'s management plane uses a private CA and
certificates for all internal communication. The client certificates
are **automatically rotated on a schedule**, providing a strong method
for reducing the effect of a compromised node. There is an option to
reduce the default time interval of 90 days to a shorter interval,
however shorter intervals do add stress to the UCP cluster. To adjust
the certificate rotation schedule, go to Admin -\> Admin Settings -\>
Swarm and scroll down.

[[https://success.docker.com/article/security-best-practices]{.ul}](https://success.docker.com/article/security-best-practices)

### **Answer 48: b**

*Explanation*

When you deploy UCP, it starts running a globally scheduled service
called ucp-agent. This service monitors the node where it's running and
starts and stops UCP services, based on whether the node is a manager or
a worker node.

If the node is a:

· **Manager**: the ucp-agent service automatically starts serving all
UCP components, including the UCP web UI and data stores used by UCP.
The ucp-agent accomplishes this by deploying several containers on the
node.

· **Worker**: on worker nodes, the ucp-agent service starts serving a
proxy service that ensures only authorized users and other UCP services
can run Docker commands in that node.

[[https://docs.docker.com/ee/ucp/ucp-architecture/\#ucp-internal-components]{.ul}](https://docs.docker.com/ee/ucp/ucp-architecture/#ucp-internal-components)
