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

### **Answer 13: c**

*Explanation*

To save one or more images to a tar archive (streamed to STDOUT by
default) use:

docker save \[OPTIONS\] IMAGE \[IMAGE\...\]

The achieve can be distributed through different channels such as:
central file server, version-control system, sent it to you over email
or shared it via flash drive.

[[https://docs.docker.com/engine/reference/commandline/save/]{.ul}](https://docs.docker.com/engine/reference/commandline/save/)

Docker provides a command to load images into Docker from a file. With
this tool, you can load images that you acquired through other channels.

[[https://docs.docker.com/engine/reference/commandline/image_load/]{.ul}](https://docs.docker.com/engine/reference/commandline/image_load/)

### **Answer 14: d**

*Explanation*

To create a tag TARGET_IMAGE that refers to SOURCE_IMAGE use:

docker tag SOURCE_IMAGE\[:TAG\] TARGET_IMAGE\[:TAG\]

[[https://docs.docker.com/engine/reference/commandline/tag/]{.ul}](https://docs.docker.com/engine/reference/commandline/tag/)

### **Answer 15: a**

*Explanation*

The default filename is **Dockerfile** (without an extension), and using
the default can make various tasks easier while working with containers.

However, you can name it whatever you like.

For example, check the following output:

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/dockerfileName.png)

[[https://stackoverflow.com/questions/26077543/how-to-name-dockerfiles]{.ul}](https://stackoverflow.com/questions/26077543/how-to-name-dockerfiles)

### **Answer 16: b**

*Explanation*

The WORKDIR instruction can be used multiple times in a Dockerfile.

· If a relative path is provided, it will be relative to the path of the
previous WORKDIR instruction.

· If the WORKDIR doesn't exist, it will be created even if it's not used
in any subsequent Dockerfile instruction.

The WORKDIR instruction can resolve environment variables previously set
using ENV. You can only use environment variables explicitly set in the
Dockerfile. For example:

ENV DIRPATH /path

WORKDIR \$DIRPATH/\$DIRNAME

RUN pwd

[[https://docs.docker.com/engine/reference/builder/\#workdir]{.ul}](https://docs.docker.com/engine/reference/builder/#workdir)

### **Answer 17: b**

*Explanation*

**Warning**

When building an image, do not use your root directory, /, as the PATH
as it causes the build to transfer the entire contents of your hard
drive to the Docker daemon.

[[https://docs.docker.com/engine/reference/builder/]{.ul}](https://docs.docker.com/engine/reference/builder/)

### **Answer 18: b**

*Explanation*

The HEALTHCHECK instruction tells Docker how to test a container to
check that it is still working. This can detect cases such as a web
server that is stuck in an infinite loop and unable to handle new
connections, even though the server process is still running.

[[https://docs.docker.com/engine/reference/builder/\#healthcheck]{.ul}](https://docs.docker.com/engine/reference/builder/#healthcheck)

### **Answer 19: a**

*Explanation*

To create a new image from a container's changes use:

docker commit \[OPTIONS\] CONTAINER \[REPOSITORY\[:TAG\]\]

It can be useful to commit a container's file changes or settings into a
new image.

This allows you to export a working dataset to another server.

Still, it is better to use Dockerfiles to manage your images in a
documented and maintainable way. The Version Control can be used mainly
for text-based files such as Dockerfiles, docker-compose.yml, and
configuration files. Small binaries can also be kept in the same version
control. Examples of version control are git, svn, Team Foundation
Server, Azure DevOps, and Clear Case.

[[https://success.docker.com/article/dev-pipeline]{.ul}](https://success.docker.com/article/dev-pipeline)

### **Answer 20: c**

*Explanation*

Docker can build images automatically by reading the instructions from a
Dockerfile.

A Dockerfile is a text document that contains all the commands a user
could call on the command line to assemble an image.

Using docker build users can create an automated build that executes
several command-line instructions in succession.

[[https://docs.docker.com/engine/reference/builder/]{.ul}](https://docs.docker.com/engine/reference/builder/)

### **Answer 21: d**

*Explanation*

LABEL

LABEL \<key\>=\<value\> \<key\>=\<value\> \<key\>=\<value\> \...

The LABEL instruction adds metadata to an image. A LABEL is a key-value
pair.

Example:

LABEL version=\"1.0\"

[[https://docs.docker.com/engine/reference/builder/\#label]{.ul}](https://docs.docker.com/engine/reference/builder/#label)

### **Answer 22: a**

*Explanation*

A **container** is a runtime instance of a docker image.

A Docker container consists of

· A Docker image

· An execution environment

· A standard set of instructions

The concept is borrowed from Shipping Containers, which define a
standard to ship goods globally. Docker defines a standard to ship
software.

[[https://docs.docker.com/glossary/]{.ul}](https://docs.docker.com/glossary/)

### **Answer 23: a**

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

https://docs.docker.com/engine/reference/builder/\#expose

The ENV instruction sets the environment variable \<key\> to the value
\<value\>. This value will be in the environment for all subsequent
instructions in the build stage.

### **Answer 24: b**

*Explanation*

ENV

ENV \<key\> \<value\>

ENV \<key\>=\<value\> \...

The ENV instruction sets the environment variable \<key\> to the value
\<value\>. This value will be in the environment for all subsequent
instructions in the build stage.

Also, the environment variables set using ENV will persist when a
container is run from the resulting image. You can view the values using
docker inspect, and change them using docker run \--env
\<key\>=\<value\>.

https://docs.docker.com/engine/reference/builder/\#env

### **Answer 25: d**

*Explanation*

CMD instruction allows you to set a default command, which will be
executed only when you run container without specifying a command. If
Docker container runs with a command, the default command will be
ignored. If Dockerfile has more than one CMD instruction, all but last
CMD instructions are ignored.

ENTRYPOINT instruction allows you to configure a container that will run
as an executable. It looks similar to CMD, because it also allows you to
specify a command with parameters. The difference is ENTRYPOINT command
and parameters are not ignored when Docker container runs with command
line parameters. (There is a way to ignore ENTTRYPOINT, but it is
unlikely that you will do it.)

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/dockerBuildTest.png)

https://docs.docker.com/engine/reference/builder
