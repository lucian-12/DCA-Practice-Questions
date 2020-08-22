### **Answer 1: a**

*Explanation*

When possible, overlay2 is the recommended storage driver.

When installing Docker for the first time, overlay2 is used by default.
Previously, aufs was used by default when available, but this is no
longer the case. If you want to use aufs on new installations going
forward, you need to explicitly configure it, and you may need to
install extra packages, such as linux-image-extra.

[[https://docs.docker.com/storage/storagedriver/select-storage-driver/\#docker-engine\-\--community]{.ul}](https://docs.docker.com/storage/storagedriver/select-storage-driver/#docker-engine---community)

### **Answer 2: b**

*Explanation*

To display system-wide information use:

    docker info \[OPTIONS\]

This command displays system wide information regarding the Docker
installation. Information displayed includes the kernel version, number
of containers and images.

Depending on the storage driver in use, additional information can be
shown, such as pool name, data file, metadata file, data space used,
total data space, metadata space used, and total metadata space.

https://docs.docker.com/engine/reference/commandline/info/

### **Answer 3: a**

*Explanation*

Device Mapper is a kernel-based framework that underpins many advanced
volume management technologies on Linux.

Docker's devicemapper storage driver leverages the thin provisioning and
snapshotting capabilities of this Device Mapper framework for image and
container management.

Device Mapper configuration modes:

· l**oop-lvm mode** - is only appropriate for testing. The loop-lvm mode
makes use of a 'loopback' mechanism that allows files on the local disk
to be read from and written to as if they were an actual physical disk
or block device.

· **direct-lvm mode** - Production hosts using the devicemapper storage
driver must use direct-lvm mode. This is faster than using loopback
devices, uses system resources more efficiently, and block devices can
grow as needed. However, more setup is required than in loop-lvm mode.

[[https://docs.docker.com/storage/storagedriver/device-mapper-driver/\#configure-loop-lvm-mode-for-testing]{.ul}](https://docs.docker.com/storage/storagedriver/device-mapper-driver/#configure-loop-lvm-mode-for-testing)

### **Answer 4: b**

*Explanation*

Particular storage-driver can be configured with options specified
with \--storage-opt flags. Options for devicemapper are prefixed with
dm.

[[https://docs.docker.com/engine/reference/commandline/dockerd/\#options-per-storage-driver]{.ul}](https://docs.docker.com/engine/reference/commandline/dockerd/#options-per-storage-driver)

Device Mapper configuration modes:

· **loop-lvm mode** - is only appropriate for testing. The loop-lvm mode
makes use of a 'loopback' mechanism that allows files on the local disk
to be read from and written to as if they were an actual physical disk
or block device.

· **direct-lvm mode** - Production hosts using the devicemapper storage
driver must use direct-lvm mode. This is faster than using loopback
devices, uses system resources more efficiently, and block devices can
grow as needed. However, more setup is required than in loop-lvm mode.

[[https://docs.docker.com/storage/storagedriver/device-mapper-driver/\#configure-loop-lvm-mode-for-testing]{.ul}](https://docs.docker.com/storage/storagedriver/device-mapper-driver/#configure-loop-lvm-mode-for-testing)

### **Answer 5: b**

*Explanation*

The devicemapper driver uses block devices dedicated to Docker and
operates at the block level, rather than the file level.

With Docker 17.06 and higher, Docker can manage the block device for
you, simplifying configuration of direct-lvm mode. This is appropriate
for fresh Docker setups only.

You can only use a single block device. If you need to use multiple
block devices, configure direct-lvm mode manually instead.

[[https://docs.docker.com/storage/storagedriver/device-mapper-driver/\#configure-direct-lvm-mode-for-production]{.ul}](https://docs.docker.com/storage/storagedriver/device-mapper-driver/#configure-direct-lvm-mode-for-production)

### **Answer 6: a**

*Explanation*

The Docker daemon persists all data in a single directory. This tracks
everything related to Docker, including containers, images, volumes,
service definition, and secrets.

By default this directory is:

    · /var/lib/docker on Linux.

    · C:\\ProgramData\\docker on Windows.

[[https://docs.docker.com/config/daemon/\#docker-daemon-directory]{.ul}](https://docs.docker.com/config/daemon/#docker-daemon-directory)

Usually, on Linux distributions:

\"/etc\" is used for configurations (.conf files etc). here you find all
the configs and settings for your system.

\"/var\" is usually used for log files, \'temporary\' files (like mail
spool, printer spool, etc), databases, and all other data not tied to a
specific user. Logs are usually in \"/var/log\", databases in
\"/var/lib\" (mysql - \"/var/lib/mysql\"), etc.

[[https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard]{.ul}](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)

### **Answer 7: a**

*Explanation*

As opposed to volumes and bind mounts, a tmpfs mount is temporary, and
only persisted in the host memory. When the container stops,
the tmpfs mount is removed, and files written there won't be persisted.

This is useful to temporarily store sensitive files that you don't want
to persist in either the host or the container writable layer.

[[https://docs.docker.com/storage/tmpfs/]{.ul}](https://docs.docker.com/storage/tmpfs/)

### **Answer 8: a**

*Explanation*

A PV can have a class, which is specified by setting
the **storageClassName** attribute to the name of a StorageClass. A PV
of a particular class can only be bound to PVCs requesting that class. A
PV with no storageClassName has no class and can only be bound to PVCs
that request no particular class.

[[https://kubernetes.io/docs/concepts/storage/persistent-volumes/\#class]{.ul}](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#class)

### **Answer 9: a**

*Explanation*

**Container size on disk**

To view the approximate size of a running container, you can use the
docker ps -s command. Two different columns relate to size.

· **size**: the amount of data (on disk) that is used for the writable
layer of each container.

· **virtual size**: the amount of data used for the read-only image data
used by the container plus the container's writable layer size. Multiple
containers may share some or all read-only image data. Two containers
started from the same image share 100% of the read-only data, while two
containers with different images which have layers in common share those
common layers. Therefore, you can't just total the virtual sizes. This
over-estimates the total disk usage by a potentially non-trivial amount.

[[https://docs.docker.com/storage/storagedriver/\#container-size-on-disk]{.ul}](https://docs.docker.com/storage/storagedriver/#container-size-on-disk)

**Copy-on-write** is a strategy of sharing and copying files for maximum
efficiency. If a file or directory exists in a lower layer within the
image, and another layer (including the writable layer) needs read
access to it, it just uses the existing file.

[[https://docs.docker.com/storage/storagedriver/\#the-copy-on-write-cow-strategy]{.ul}](https://docs.docker.com/storage/storagedriver/#the-copy-on-write-cow-strategy)

### **Answer 10: a**

*Explanation*

A Docker image is built up from a series of layers. Each layer
represents an instruction in the image's Dockerfile. Each layer except
the very last one is read-only.

Each container **has its own writable container layer**, and all changes
are stored in this container layer.

However, multiple containers can share access to the same underlying
image and yet have their own data state. The diagram below shows
multiple containers sharing the same Ubuntu 18.04 image.

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageLayers.png)

[[https://docs.docker.com/storage/storagedriver/\#container-and-layers]{.ul}](https://docs.docker.com/storage/storagedriver/#container-and-layers)

### **Answer 11: c**

*Explanation*

The major difference between a container and an image is **the top
writable layer**. All writes to the container that add new or modify
existing data are stored in this writable layer. When the container is
deleted, the writable layer is also deleted. The underlying image
remains unchanged.

Because each container has its own writable container layer, and all
changes are stored in this container layer, multiple containers can
share access to the same underlying image and yet have their own data
state. The diagram below shows multiple containers sharing the same
Ubuntu 18.04 image.

Docker uses storage drivers to manage the contents of the image layers
and the writable container layer. Each storage driver handles the
implementation differently, but all drivers use stackable image layers
and the **copy-on-write** (CoW) strategy.

[[https://docs.docker.com/storage/storagedriver/\#container-and-layers]{.ul}](https://docs.docker.com/storage/storagedriver/#container-and-layers)

### **Answer 12: b**

*Explanation*

Docker uses **storage drivers** to manage the contents of the image
layers and the writable container layer. Each storage driver handles the
implementation differently, but all drivers use stackable image layers
and the copy-on-write (CoW) strategy.

[[https://docs.docker.com/storage/storagedriver/\#container-and-layers]{.ul}](https://docs.docker.com/storage/storagedriver/#container-and-layers)

### **Answer 13: b**

*Explanation*

A Docker image is built up from **a series of layers**. Each layer
represents an instruction in the image's Dockerfile.

Each layer except the very last one is read-only.

Each layer is only a **set of differences from the layer before it**.

[[https://docs.docker.com/storage/storagedriver/\#images-and-layers]{.ul}](https://docs.docker.com/storage/storagedriver/#images-and-layers)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageLayers.png)

### **Answer 14: b**

*Explanation*

When an existing file in a container is modified, the storage driver
performs a copy-on-write operation. The specifics steps involved depend
on the specific storage driver. For the aufs, overlay, and overlay2
drivers, the copy-on-write operation follows this rough sequence:

· Search through the image layers for the file to update. The process
starts at the newest layer and works down to the base layer one layer at
a time. When results are found, they are added to a cache to speed
future operations.

· Perform a copy_up operation on the first copy of the file that is
found, to copy the file to the container's writable layer.

· Any modifications are made to this copy of the file, and the container
cannot see the read-only copy of the file that exists in the lower
layer.

[[https://docs.docker.com/storage/storagedriver/\#copying-makes-containers-efficient]{.ul}](https://docs.docker.com/storage/storagedriver/#copying-makes-containers-efficient)

### **Answer 15: b**

*Explanation*

A user creates, or in the case of dynamic provisioning, has already
created, a PersistentVolumeClaim with a specific amount of storage
requested and with certain access modes. A control loop in the master
watches for new PVCs, finds a matching PV (if possible), and binds them
together. If a PV was dynamically provisioned for a new PVC, the loop
will always bind that PV to the PVC. Otherwise, the user will always get
at least what they asked for, but the volume may be in excess of what
was requested. Once bound, PersistentVolumeClaim binds are exclusive,
regardless of how they were bound. A PVC to PV binding is a **one-to-one
mapping**, using a ClaimRef which is a bi-directional binding between
the PersistentVolume and the PersistentVolumeClaim.

[[https://kubernetes.io/docs/concepts/storage/persistent-volumes/\#binding]{.ul}](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#binding)

### **Answer 16: d**

*Explanation*

Anonymous volumes can be cleaned up in two ways. First, anonymous
volumes are automatically deleted when the container they were created
for are automatically cleaned up. This happens when containers are
deleted via the docker run \--rm or docker rm -v flags.

Remove one or more containers

    docker rm \[OPTIONS\] CONTAINER \[CONTAINER\...\]

Second, they can be manually deleted by issuing a docker volume remove
command:

    docker volume rm \[OPTIONS\] VOLUME \[VOLUME\...\]

[[https://docs.docker.com/engine/reference/commandline/volume_rm/]{.ul}](https://docs.docker.com/engine/reference/commandline/volume_rm/)

### **Answer 17: a**

*Explanation*

The docker run command provides a flag, \--volumes-from, that will copy
the mount definitions from one or more containers to the new container.

By combining this flag and volumes, you can build shared-state
relationships in a host-independent way.

[[https://docs.docker.com/engine/reference/commandline/run/\#mount-volumes-from-container\-\--volumes-from]{.ul}](https://docs.docker.com/engine/reference/commandline/run/#mount-volumes-from-container---volumes-from)

### **Answer 18: a**

*Explanation*

-V and \--volumes are incorrect flags.

Output message:

    unknown shorthand flag: \'V\' in -V

    unknown flag: \--volumes

To mount a volume use -v or \--volume.

These flags consist of three fields, separated by colon characters (:).
The fields must be in the correct order, and the meaning of each field
is not immediately obvious.

· In the case of named volumes, the first field is the name of the
volume, and is unique on a given host machine. For anonymous volumes,
the first field is omitted.

· The second field is the path where the file or directory are mounted
in the container.

· The third field is optional, and is a comma-separated list of options,
such as ro. These options are discussed below.

If you start a container with a volume that does not yet exist, Docker
creates the volume for you. The following example mounts the volume
myvol2 into /app/ in the container.

    \$ docker run -d \\

      \--name devtest \\

      -v myvol2:/app \\

      nginx:latest

[[https://docs.docker.com/storage/volumes/]{.ul}](https://docs.docker.com/storage/volumes/)

### **Answer 19: d**

*Explanation*

To mount a volume use -v or \--volume.

These flags consist of three fields, separated by colon characters (:).
The fields must be in the correct order, and the meaning of each field
is not immediately obvious.

· In the case of named volumes, the first field is the name of the
volume, and is unique on a given host machine. For anonymous volumes,
the first field is omitted.

· The second field is the path where the file or directory are mounted
in the container.

· The third field is optional, and is a comma-separated list of options,
such as ro. These options are discussed below.

If you start a container with a volume that does not yet exist, Docker
creates the volume for you. The following example mounts the volume
myvol2 into /app/ in the container.

    \$ docker run -d \\

      \--name devtest \\

      -v myvol2:/app \\

      nginx:latest

[[https://docs.docker.com/storage/volumes/]{.ul}](https://docs.docker.com/storage/volumes/)

### **Answer 20: b**

*Explanation*

Volumes and bind mounts let you share files between the host machine and
container so that you can persist data even after the container is
stopped.

However, if you're running Docker on Linux, you have a third
option: **tmpfs** mounts.

As opposed to volumes and bind mounts, a tmpfs mount is temporary, and
only persisted in the host memory. When the container stops, the tmpfs
mount is removed, and files written there won't be persisted.

Therefore, this kind of mount is not recommended for storing state such
as the visitor counts.

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/volume.png)

[[https://docs.docker.com/storage/tmpfs/]{.ul}](https://docs.docker.com/storage/tmpfs/)

### **Answer 21: c**

*Explanation*

To manage volume, you could use:

    docker volume COMMAND COMMAND

You can use subcommands to create, inspect, list, remove, or prune
volumes.

**Create a volume**

docker volume create

**Display detailed information on one or more volumes**

docker volume inspect

**List volumes**

docker volume ls

**Remove all unused local volumes**

docker volume prune

**Remove one or more volumes**

docker volume rm

[[https://docs.docker.com/engine/reference/commandline/volume/]{.ul}](https://docs.docker.com/engine/reference/commandline/volume/)

### **Answer 22: c**

*Explanation*

To inspect changes to files or directories on a container's filesystem
use:

    docker diff CONTAINER

This lists the changed files and directories in a container᾿s filesystem
since the container was created.

Three different types of change are tracked with different symbols:

    A A file or directory was added

    D A file or directory was deleted

    C A file or directory was changed

[[https://docs.docker.com/engine/reference/commandline/diff/\#description]{.ul}](https://docs.docker.com/engine/reference/commandline/diff/#description)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/diff_container.png)

### **Answer 23: c**

*Explanation*

Volumes are the preferred mechanism for persisting data generated by and
used by Docker containers. While bind mounts are dependent on the
directory structure of the host machine, volumes are completely managed
by Docker. Volumes have several advantages over bind mounts:

Volumes are easier to back up or migrate than bind mounts.

Volumes are useful for **backups**, **restores**, and **migrations**.
Use the \--volumes-from flag to create a new container that mounts that
volume.

[[https://docs.docker.com/storage/volumes/\#backup-restore-or-migrate-data-volumes]{.ul}](https://docs.docker.com/storage/volumes/#backup-restore-or-migrate-data-volumes)

### **Answer 24: b**

*Explanation*

**Populate a volume using a container**

If you start a container which creates a new volume, and the container
has files or directories in the directory to be mounted, the directory's
contents are copied into the volume.

Then, the container mounts and uses the volume, and other containers
which use the volume also have access to the pre-populated content.

To illustrate this, this example starts an nginx container and populates
the new volume nginx-vol with the contents of the container's
/usr/share/nginx/html directory, which is where Nginx stores its default
HTML content.

The \--mount and -v examples have the same end result.

    \$ docker run -d \\

      \--name=nginxtest \\

      -v nginx-vol:/usr/share/nginx/html \\

      nginx:latest

[[https://docs.docker.com/storage/volumes/\#populate-a-volume-using-a-container]{.ul}](https://docs.docker.com/storage/volumes/#populate-a-volume-using-a-container)

### **Answer 25: a, c**

*Explanation*

Bind mounts have been around since the early days of Docker. Bind mounts
have limited functionality compared to volumes. When you use a bind
mount, a file or directory on the host machine is mounted into a
container.

The file or directory is referenced by its **full or relative path** on
the host machine. By contrast, when you use a volume, a new directory is
created within Docker's storage directory on the host machine, and
Docker manages that directory's contents.

Use the following command to bind-mount the target/ directory into your
container at /app/. Run the command from within the source directory.
The \$(pwd) sub-command expands to the current working directory on
Linux or macOS hosts.

The \--mount and -v examples below produce the same result. You can't
run them both unless you remove the devtest container after running the
first one.

    \$ docker run -d \\

      -it \\

      \--name devtest \\

      \--mount type=bind,source=\"\$(pwd)\"/target,target=/app \\

      nginx:latest

 

    \$ docker run -d \\

      -it \\

      \--name devtest \\

      -v \"\$(pwd)\"/target:/app \\

      nginx:latest

[[https://docs.docker.com/storage/bind-mounts/\#differences-between\--v-and\-\--mount-behavior]{.ul}](https://docs.docker.com/storage/bind-mounts/#differences-between--v-and---mount-behavior)

### **Answer 26: c**

*Explanation*

Remove one or more images

    docker image rm \[OPTIONS\] IMAGE \[IMAGE\...\]

[[https://docs.docker.com/engine/reference/commandline/image_rm/]{.ul}](https://docs.docker.com/engine/reference/commandline/image_rm/)

### **Answer 27: c**

*Explanation*

In the context of the Docker registry, **garbage collection** is the
process of removing blobs from the filesystem when they are no longer
referenced by a manifest. Blobs can include both layers and manifests.

Registry data can occupy considerable amounts of disk space. In
addition, garbage collection can be a security consideration, when it is
desirable to ensure that certain layers no longer exist on the
filesystem.

[[https://docs.docker.com/registry/garbage-collection/\#about-garbage-collection]{.ul}](https://docs.docker.com/registry/garbage-collection/#about-garbage-collection)

### **Answer 28: a**

*Explanation*

The docker system df command displays information regarding the amount
of disk space used by the docker daemon.

By default the command will just show a summary of the data used
including images, containers and local volumes:

    \$ docker system df

[[https://docs.docker.com/engine/reference/commandline/system_df/\#examples]{.ul}](https://docs.docker.com/engine/reference/commandline/system_df/#examples)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/sysDiff.png)

### **Answer 29: c**

*Explanation*

To remove all unused local volumes use:

    docker volume prune \[OPTIONS\]

Unused local volumes are those which are not referenced by any
containers

[[https://docs.docker.com/engine/reference/commandline/volume_prune/]{.ul}](https://docs.docker.com/engine/reference/commandline/volume_prune/)

### **Answer 30: b**

*Explanation*

A **PersistentVolume** (PV) is a piece of storage in the cluster that
has been provisioned by an administrator or dynamically provisioned
using Storage Classes.

[[https://kubernetes.io/docs/concepts/storage/persistent-volumes/\#persistent-volumes]{.ul}](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volumes)

**Dynamic volume provisioning** allows storage volumes to be created
on-demand. Without dynamic provisioning, cluster administrators have to
manually make calls to their cloud or storage provider to create new
storage volumes, and then create PersistentVolume objects to represent
them in Kubernetes. The dynamic provisioning feature eliminates the need
for cluster administrators to pre-provision storage. Instead, it
automatically provisions storage when it is requested by users.

[[https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/\#enabling-dynamic-provisioning]{.ul}](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/#enabling-dynamic-provisioning)

### **Answer 31: a**

*Explanation*

To display detailed information on one or more images use:

    docker image inspect \[OPTIONS\] IMAGE \[IMAGE\...\]

[[https://docs.docker.com/engine/reference/commandline/image_inspect/]{.ul}](https://docs.docker.com/engine/reference/commandline/image_inspect/)

### **Answer 32: a**

*Explanation*

**Claims** will remain unbound indefinitely if a matching volume does
not exist. Claims will be bound as matching volumes become available.
For example, a cluster provisioned with many 50Gi PVs would not match a
PVC requesting 100Gi. The PVC can be bound when a 100Gi PV is added to
the cluster.

[[https://kubernetes.io/docs/concepts/storage/persistent-volumes/\#binding]{.ul}](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#binding)

### **Answer 33: b**

*Explanation*

As opposed to volumes and bind mounts, a tmpfs mount is temporary, and
only persisted in the host memory. When the container stops,
the tmpfs mount is removed, and files written there won't be persisted.

This is useful to temporarily store sensitive files that you don't want
to persist in either the host or the container writable layer.

[[https://docs.docker.com/storage/tmpfs/]{.ul}](https://docs.docker.com/storage/tmpfs/)
