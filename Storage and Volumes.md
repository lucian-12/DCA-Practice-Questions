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
