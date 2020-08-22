### **Answer 1: d**

*Explanation*

In the Dockerfile context, The RUN instruction will execute any commands
in a new layer on top of the current image and commit the results.

Layering RUN instructions and generating commits conforms to the core
concepts of Docker where commits are cheap and containers can be created
from any point in an image's history, much like source control.

https://docs.docker.com/engine/reference/builder/\#run

### **Answer 2: a**

*Explanation*

There can only be one CMD instruction in a Dockerfile. If you list more
than one CMD then only the last CMD will take effect.

The main purpose of a CMD is to provide defaults for an executing
container.

[[https://docs.docker.com/engine/reference/builder/\#cmd]{.ul}](https://docs.docker.com/engine/reference/builder/#cmd)

### **Answer 3: b**

*Explanation*

To tag the image into multiple repositories after the build, add
multiple -t parameters when you run the build command:

\$ docker build -t myrepo/myapp:1.0.2 -t myrepo/myapp:latest .

https://docs.docker.com/engine/reference/builder/\#run\#usage

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageTag2.png)

### **Answer 4: d**

*Explanation*

Note: Every shell command returns a status code

The HEALTHCHECK instruction tells Docker how to test a container to
check that it is still working.

The HEALTHCHECK instruction has two forms:

· HEALTHCHECK \[OPTIONS\] CMD command (check container health by running
a command inside the container)

· HEALTHCHECK NONE (disable any healthcheck inherited from the base
image)

When a container has a healthcheck specified, it has a health status in
addition to its normal status.

The command after the CMD keyword can be either a shell command (e.g.
HEALTHCHECK CMD /bin/check-running) or an exec array (as with other
Dockerfile commands; see e.g. ENTRYPOINT for details).

[[https://docs.docker.com/engine/reference/builder/\#healthcheck]{.ul}](https://docs.docker.com/engine/reference/builder/#healthcheck)

### **Answer 5: b**

*Explanation*

To remove one or more images use:

docker rmi \[OPTIONS\] IMAGE \[IMAGE\...\]

You cannot remove an image of a running container unless you use
the --force or -f option.

[[https://docs.docker.com/engine/reference/commandline/rmi/]{.ul}](https://docs.docker.com/engine/reference/commandline/rmi/)

This removes (and un-tags) one or more images from the host node. If an
image has multiple tags, using this command with the tag as a parameter
only removes the tag. If the tag is the only one for the image, both the
image and the tag are removed.

This does not remove images from a registry.

### **Answer 6: a**

*Explanation*

The docker build command builds an image from a **Dockerfile** and
a **context**.

The build's context is the set of files at a specified location PATH or
URL. The PATH is a directory on your local filesystem. The URL is a Git
repository location.

A context is processed recursively. So, a PATH includes any
subdirectories and the URL includes the repository and its submodules.

This example shows a build command that uses the current directory as
context:

\$ docker build .

Sending build context to Docker daemon  6.51 MB

\...

You use the -f flag with docker build to point to a Dockerfile anywhere
in your file system.

\$ docker build -f /path/to/a/Dockerfile .

The build is run by the Docker daemon. The first thing a build process
does is send the entire context (recursively) to the daemon.

In most cases, it's best to start with an empty directory as context and
keep your Dockerfile in that directory. Add only the files needed for
building the Dockerfile.

[[https://docs.docker.com/engine/reference/builder/]{.ul}](https://docs.docker.com/engine/reference/builder/)

### **Answer 7: c**

*Explanation*

Pull an image or a repository from a registry

docker image pull     

Or

docker pull \[OPTIONS\] NAME\[:TAG\|\@DIGEST\]

[[https://docs.docker.com/engine/reference/commandline/pull/]{.ul}](https://docs.docker.com/engine/reference/commandline/pull/)

### **Answer 8: b**

*Explanation*

Images and containers

Fundamentally, a container is nothing but a running process, with some
added encapsulation features applied to it in order to keep it isolated
from the host and from other containers.

An **image** includes everything needed to run an application - the code
or binary, runtimes, dependencies, and any other filesystem objects
required.

[[https://docs.docker.com/get-started/\#images-and-containers]{.ul}](https://docs.docker.com/get-started/#images-and-containers)

### **Answer 9: a**

*Explanation*

EXPOSE \<port\> \[\<port\>/\<protocol\>\...\]

The EXPOSE instruction informs Docker that the container listens on the
specified network ports at runtime. You can specify whether the port
listens on TCP or UDP, and the default is TCP if the protocol is not
specified.

The EXPOSE instruction does not actually publish the port. It functions
as a type of documentation between the person who builds the image and
the person who runs the container, about which ports are intended to be
published. To actually publish the port when running the container, use
the -p flag on docker run to publish and map one or more ports, or the
-P flag to publish all exposed ports and map them to high-order ports.

<https://docs.docker.com/engine/reference/builder/#expose>

### **Answer 10: b**

*Explanation*

You can specify a repository and tag at which to save the new image if
the build succeeds:

\$ docker build -t myrepo/myapp .

The output could look like the following:

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageTag.png)

To tag the image into multiple repositories after the build, add
multiple -t parameters when you run the build command:

\$ docker build -t shykes/myapp:1.0.2 -t shykes/myapp:latest .

[https://docs.docker.com/engine/reference/builder/\#run\#usage](https://docs.docker.com/engine/reference/builder/#run)

### **Answer 11: c**

*Explanation*

By default, when you push an image to DTR, the Docker CLI client doesn't
sign the image.

You can configure the Docker CLI client to sign the images you push to
DTR. This allows whoever pulls your image to validate if they are
getting the image you created, or a forged one.

To sign an image you can run:

export DOCKER_CONTENT_TRUST=1

### **Answer 12: a**

*Explanation*

To show untagged images, or dangling, use:

docker images \--filter \"dangling=true\"

This will display untagged images that are the leaves of the images tree
(not intermediary layers). These images occur when a new build of an
image takes the repo:tag away from the image ID, leaving it as
\<none\>:\<none\> or untagged. A warning will be issued if trying to
remove an image when a container is presently using it. By having this
flag it allows for batch cleanup.

[[https://docs.docker.com/engine/reference/commandline/images/\#filtering]{.ul}](https://docs.docker.com/engine/reference/commandline/images/#filtering)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageInspectFilter.png)
