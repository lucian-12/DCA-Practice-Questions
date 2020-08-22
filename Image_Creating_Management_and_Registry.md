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

    $ docker build -t myrepo/myapp:1.0.2 -t myrepo/myapp:latest .

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

    docker rmi [OPTIONS] IMAGE [IMAGE\...]

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

    $ docker build .

    Sending build context to Docker daemon  6.51 MB

    \...

You use the -f flag with docker build to point to a Dockerfile anywhere
in your file system.

    $ docker build -f /path/to/a/Dockerfile .

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

    docker pull [OPTIONS] NAME[:TAG\|\@DIGEST]

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

    EXPOSE <port> [<port>/<protocol>\...]

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

    $ docker build -t myrepo/myapp .

The output could look like the following:

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageTag.png)

To tag the image into multiple repositories after the build, add
multiple -t parameters when you run the build command:

    $ docker build -t shykes/myapp:1.0.2 -t shykes/myapp:latest .

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

    docker images \--filter "dangling=true"

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

    docker save [OPTIONS] IMAGE [IMAGE\...]

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

    docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

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

    WORKDIR $DIRPATH/$DIRNAME

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

    docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

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

    LABEL <key>=<value> <key>=<value> <key>=<value> \...

The LABEL instruction adds metadata to an image. A LABEL is a key-value
pair.

Example:

    LABEL version="1.0"

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

    EXPOSE <port> [<port>/<protocol>\...]

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

    ENV <key> <value>

    ENV <key>=<value> \...

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

### **Answer 26: b**

*Explanation*

Note: Don't confuse RUN with CMD. RUN actually runs a command and
commits the result; CMD does not execute anything at build time, but
specifies the intended command for the image.

[[https://docs.docker.com/engine/reference/builder/\#cmd]{.ul}](https://docs.docker.com/engine/reference/builder/#cmd)

### **Answer 27: c**

*Explanation*

To create a tag TARGET_IMAGE that refers to SOURCE_IMAGE use:

    docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

Example:

To tag a local image with name "myimage" into the "myrepositroy"
repository with "version1.0":

    docker tag myimage myrepositroy/myimage:version1.0

[[https://docs.docker.com/engine/reference/commandline/tag/]{.ul}](https://docs.docker.com/engine/reference/commandline/tag/)

### **Answer 28: d**

*Explanation*

    docker images [OPTIONS] [REPOSITORY[:TAG]]

The default docker images will show all top-level images, their
repository and tags, and their size.

You can use \--all, -a to show all images (default hides intermediate
images)

[[https://docs.docker.com/engine/reference/commandline/images/]{.ul}](https://docs.docker.com/engine/reference/commandline/images/)

### **Answer 29: a**

*Explanation*

In the Dockerfile context, The RUN instruction will execute any commands
in a new layer on top of the current image and commit the results.

Layering RUN instructions and generating commits conforms to the core
concepts of Docker where commits are cheap and containers can be created
from any point in an image's history, much like source control.

<https://docs.docker.com/engine/reference/builder/#run>

### **Answer 30: c**

*Explanation*

To display detailed information on one or more images use:

    docker image inspect [OPTIONS] IMAGE [IMAGE\...]

[[https://docs.docker.com/engine/reference/commandline/image_inspect/]{.ul}](https://docs.docker.com/engine/reference/commandline/image_inspect/)

### **Answer 31: d**

*Explanation*

Docker inspect provides detailed information on constructs controlled by
Docker.

By default, docker inspect will render results in a JSON array.

To display detailed information on one or more images use:

    docker image inspect [OPTIONS] IMAGE [IMAGE\...]

The options are:

    \--format , -f 

Format the output using the given Go template

For the most part, you can pick out any field from the JSON in a fairly
straightforward manner using the --format parameter.

    $ docker inspect \--format='{{.LogPath}}' $INSTANCE_ID

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageInspectFormatpng.png)

[[https://docs.docker.com/engine/reference/commandline/inspect/]{.ul}](https://docs.docker.com/engine/reference/commandline/inspect/)

### **Answer 32: b**

*Explanation*

The build is run by the Docker daemon, not by the CLI.

The first thing a build process does is send the entire context
(recursively) to the daemon.

[[https://docs.docker.com/engine/reference/builder/]{.ul}](https://docs.docker.com/engine/reference/builder/)

### **Answer 33: a, b, c**

*Explanation*

By default, when you push an image to DTR, the Docker CLI client doesn't
sign the image.

You can configure the Docker CLI client to sign the images you push to
DTR. This allows whoever pulls your image to validate if they are
getting the image you created, or a forged one.

To sign an image you can run:

    export DOCKER_CONTENT_TRUST=1

    docker push <dtr-domain>/<repository>/<image>:<tag>

This pushes the image to DTR and creates trust metadata. It also creates
public and private key pairs to sign the trust metadata, and push that
metadata to the Notary Server internal to DTR.

![img](https://github.com/lucian-12/DCA-Practice-Questions/blob/master/img/imageSignedpng.png)

Sign images that UCP can trust

With the command above you can sign your DTR images, but UCP doesn't
trust them because it can't tie the private key you're using to sign the
images to your UCP account.

To sign images in a way that UCP trusts them you need to:

· Configure your Notary client

· Initialize trust metadata for the repository

· Delegate signing to the keys in your UCP client bundle

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 34: a**

*Explanation*

**Prune images**

The docker image prune command allows you to clean up unused images. By
default, docker image prune only cleans up dangling images. A dangling
image is one that is not tagged and is not referenced by any container.
To remove dangling images:

    $ docker image prune

To remove all images which are not used by existing containers, use the
-a flag:

    $ docker image prune -a

[[https://docs.docker.com/config/pruning/\#prune-images]{.ul}](https://docs.docker.com/config/pruning/#prune-images)

### **Answer 35: c**

*Explanation*

    EXPOSE <port> [<port>/<protocol>\...]

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

### **Answer 36: d**

*Explanation*

When an image is updated or rebuilt,
only **layers** that **change** need to be updated, and unchanged layers
are cached locally. This is part of why Docker images are so fast and
lightweight. The sizes of each layer add up to equal the size of the
final image.

An **image** does not have state and it never changes.

[[https://docs.docker.com/glossary/]{.ul}](https://docs.docker.com/glossary/)

FROM can appear multiple times within a single Dockerfile to create
multiple images or use one build stage as a dependency for another.

[[https://docs.docker.com/engine/reference/builder/\#from]{.ul}](https://docs.docker.com/engine/reference/builder/#from)

### **Answer 37: a**

*Explanation*

To push an image or a repository to a registry use:

    docker image push [OPTIONS] NAME[:TAG]

[[https://docs.docker.com/engine/reference/commandline/image_push/]{.ul}](https://docs.docker.com/engine/reference/commandline/image_push/)

### **Answer 38: b**

*Explanation*

The FROM instruction initializes a new build stage and sets the Base
Image for subsequent instructions. As such, a valid Dockerfile must
start with a FROM instruction.

[[https://docs.docker.com/engine/reference/builder/\#from]{.ul}](https://docs.docker.com/engine/reference/builder/#from)

### **Answer 39: c**

*Explanation*

The WORKDIR instruction can be used multiple times in a Dockerfile.

If a relative path is provided, it will be relative to the path of the
previous WORKDIR instruction. For example:

    WORKDIR /a

    WORKDIR b

    WORKDIR c

    RUN pwd

The output of the final pwd command in this Dockerfile would be /a/b/c.

[[https://docs.docker.com/engine/reference/builder/\#workdir]{.ul}](https://docs.docker.com/engine/reference/builder/#workdir)

### **Answer 40: a**

*Explanation*

**Prune unused Docker objects**

Docker takes a conservative approach to cleaning up unused objects, such
as images, containers, volumes, and networks: these objects are
generally not removed unless you explicitly ask Docker to do so.

This can cause Docker to use extra disk space. For each type of object,
Docker provides a prune command. In addition, you can use docker system
prune to clean up multiple types of objects at once.

**Prune images**

The docker image prune command allows you to clean up unused images. By
default, docker image prune only cleans up dangling images. A dangling
image is one that is not tagged and is not referenced by any container.
To remove dangling images:

    $ docker image prune

To remove all images which are not used by existing containers, use the
-a flag:

    $ docker image prune -a

[[https://docs.docker.com/config/pruning/\#prune-images]{.ul}](https://docs.docker.com/config/pruning/#prune-images)

### **Answer 41: b**

*Explanation*

You can examine all the layers in an image by using the docker image
history command. It will display the following:

· Abbreviated layer ID

· Age of the layer

· Initial command of the creating container

· Total file size of that layer

[[https://docs.docker.com/engine/reference/commandline/history/]{.ul}](https://docs.docker.com/engine/reference/commandline/history/)

### **Answer 42: c**

*Explanation*

The WORKDIR instruction can be used multiple times in a Dockerfile.

If a relative path is provided, it will be relative to the path of the
previous WORKDIR instruction. For example:

    WORKDIR /a

    WORKDIR b

    WORKDIR c

    RUN pwd

The output of the final pwd command in this Dockerfile would be /a/b/c.

[[https://docs.docker.com/engine/reference/builder/\#workdir]{.ul}](https://docs.docker.com/engine/reference/builder/#workdir)

### **Answer 43: b**

*Explanation*

The RUN instruction will execute any commands in a new layer on top of
the current image and commit the results. The resulting committed image
will be used for the next step in the Dockerfile.

Layering RUN instructions and generating commits conforms to the core
concepts of Docker where commits are cheap and containers can be created
from any point in an image's history, much like source control.

Therefore, it's ok to have more than one RUN instruction.

https://docs.docker.com/engine/reference/builder/\#run

### **Answer 44: a**

*Explanation*

    ARG <name>[=<default value>]

The ARG instruction defines a variable that users can pass at build-time
to the builder with the docker build command using the \--build-arg
\<varname\>=\<value\> flag.

https://docs.docker.com/engine/reference/builder/\#arg

Unlike an ARG instruction, ENV values are always persisted in the built
image.

The variable expansion technique in this example allows you to pass
arguments from the command line and persist them in the final image by
leveraging the ENV instruction.

https://docs.docker.com/engine/reference/builder/\#run\#using-arg-variables

### **Answer 45: b**

*Explanation*

    LABEL

    LABEL <key>=<value> <key>=<value> <key>=<value> \...

The LABEL instruction adds metadata to an image. A LABEL is a key-value
pair.

Example:

    LABEL version="1.0"

[[https://docs.docker.com/engine/reference/builder/\#label]{.ul}](https://docs.docker.com/engine/reference/builder/#label)

### **Answer 46: c**

*Explanation*

The RUN instruction will execute any commands in a new layer on top of
the current image and commit the results. The resulting committed image
will be used for the next step in the Dockerfile.

ENTRYPOINT instruction allows you to configure a container that will run
as an executable. It looks similar to CMD, because it also allows you to
specify a command with parameters. The difference is ENTRYPOINT command
and parameters are not ignored when Docker container runs with command
line parameters. (There is a way to ignore ENTTRYPOINT, but it is
unlikely that you will do it.)

CMD instruction allows you to set a default command, which will be
executed only when you run container without specifying a command. If
Docker container runs with a command, the default command will be
ignored. If Dockerfile has more than one CMD instruction, all but last
CMD instructions are ignored.

EXEC is not a Dockerfile instruction.

https://docs.docker.com/engine/reference/builder/

### **Answer 47: c**

*Explanation*

To remove one or more images, use the following command:

    docker image rm [OPTIONS] IMAGE [IMAGE\...]

[[https://docs.docker.com/engine/reference/commandline/image_rm/]{.ul}](https://docs.docker.com/engine/reference/commandline/image_rm/)

### **Answer 48: a**

*Explanation*

FROM can appear multiple times within a single Dockerfile to create
multiple images or use one build stage as a dependency for another.

Each FROM instruction clears any state created by previous instructions.

[[https://docs.docker.com/engine/reference/builder/\#from]{.ul}](https://docs.docker.com/engine/reference/builder/#from)

You use multiple FROM statements in your Dockerfile for multi-stage
builds. Each FROM instruction can use a different base, and each of them
begins a new stage of the build. You can selectively copy artifacts from
one stage to another, leaving behind everything you don't want in the
final image.

[[https://docs.docker.com/develop/develop-images/multistage-build/\#use-multi-stage-builds]{.ul}](https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds)

### **Answer 49: a**

*Explanation*

To create a tag TARGET_IMAGE that refers to SOURCE_IMAGE use:

    docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]

Examples:

**Tag an image referenced by ID**

To tag a local image with ID "0e5574283393" into the "fedora" repository
with "version1.0":

    $ docker tag 0e5574283393 fedora/httpd:version1.0

**Tag an image referenced by Name**

To tag a local image with name "httpd" into the "fedora" repository with
"version1.0":

    $ docker tag httpd fedora/httpd:version1.0

Note that since the tag name is not specified, the alias is created for
an existing local version httpd:latest.

**Tag an image referenced by Name and Tag**

To tag a local image with name "httpd" and tag "test" into the "fedora"
repository with "version1.0.test":

    $ docker tag httpd:test fedora/httpd:version1.0.test

[[https://docs.docker.com/engine/reference/commandline/tag/\#examples]{.ul}](https://docs.docker.com/engine/reference/commandline/tag/#examples)

### **Answer 50: a**

*Explanation*

The RUN instruction will execute any commands in a new layer on top of
the current image and commit the results. The resulting committed image
will be used for the next step in the Dockerfile.

CMD instruction allows you to set a default command, which will be
executed only when you run container without specifying a command. If
Docker container runs with a command, the default command will be
ignored. If Dockerfile has more than one CMD instruction, all but last
CMD instructions are ignored.

https://docs.docker.com/engine/reference/builder/

### **Answer 51: c**

*Explanation*

You can use an ARG or an ENV instruction to specify variables that are
available to the RUN instruction.

Environment variables defined using the ENV instruction always override
an ARG instruction of the same name.

https://docs.docker.com/engine/reference/builder/\#run\#using-arg-variables

### **Answer 52: a, b**

*Explanation*

The ADD instruction operates similarly to the COPY instruction with two
important differences.

The ADD instruction will additionally support:

· Fetch remote source files if a URL is specified

· Auto-extraction of archive files. Extract the files of any source that
are determined to be of archive file type.

[[https://docs.docker.com/engine/reference/builder/\#add]{.ul}](https://docs.docker.com/engine/reference/builder/#add)

### **Answer 53: c, d**

*Explanation*

The ADD instruction operates similarly to the COPY instruction with two
important differences.

The ADD instruction will additionally support:

· Fetch remote source files if a URL is specified

· Auto-extraction of archive files. Extract the files of any source that
are determined to be of archive file type.

[[https://docs.docker.com/engine/reference/builder/\#add]{.ul}](https://docs.docker.com/engine/reference/builder/#add)

### **Answer 54: d**

*Explanation*

Docker Content Trust (DCT) allows you to verify the authenticity,
integrity, and publication date of Docker images that are made available
on the Docker Hub Registry.

By default, Content Trust is disabled. To enable Content Trust for
signing and verifying Docker images that you build, push to, or pull
from the Docker Hub, set the DOCKER_CONTENT_TRUST environment variable,
for example:

    export DOCKER_CONTENT_TRUST=1

[[https://docs.oracle.com/cd/E37670_01/E75728/html/section-xnz_cxk_ht.html]{.ul}](https://docs.oracle.com/cd/E37670_01/E75728/html/section-xnz_cxk_ht.html)

### **Answer 55: a**

*Explanation*

The FROM instruction initializes a new build stage and sets the Base
Image for subsequent instructions. As such, a valid Dockerfile must
start with a FROM instruction.

[[https://docs.docker.com/engine/reference/builder/\#from]{.ul}](https://docs.docker.com/engine/reference/builder/#from)

### **Answer 56: b**

*Explanation*

The FROM instruction initializes a new build stage and sets the Base
Image for subsequent instructions.

As such, a valid Dockerfile must start with a FROM instruction.

ARG is the only instruction that may precede FROM in the Dockerfile.

For example:

    ARG CODE_VERSION=latest

    FROM base:${CODE_VERSION}

[[https://docs.docker.com/engine/reference/builder/\#from]{.ul}](https://docs.docker.com/engine/reference/builder/#from#frm)

### **Answer 57: b**

*Explanation*

    ENV

    ENV <key> <value>

    ENV <key>=<value> \...

The ENV instruction sets the environment variable \<key\> to the value
\<value\>. This value will be in the environment for all subsequent
instructions in the build stage.

Also, the environment variables set using ENV will persist when a
container is run from the resulting image. You can view the values using
docker inspect, and change them using docker run \--env
\<key\>=\<value\>.

https://docs.docker.com/engine/reference/builder/\#env

### **Answer 58: d**

*Explanation*

To search the Docker Hub for images use:

    docker search [OPTIONS] TERM

The filtering flag (-f or \--filter) format is a key=value pair. If
there is more than one filter, then pass multiple flags (e.g. \--filter
is-automated=true \--filter stars=3)

The currently supported filters are:

stars (int - number of stars the image has)

is-automated (boolean - true or false) - is the image automated or not

is-official (boolean - true or false) - is the image official or not

[[https://docs.docker.com/engine/reference/commandline/search/\#filtering]{.ul}](https://docs.docker.com/engine/reference/commandline/search/#filtering)

### **Answer 59: a**

*Explanation*

By default, users with read and write access to a repository can push
the same tag multiple times to that repository. For example, when user A
pushes an image to library/wordpress:latest, there is no preventing user
B from pushing an image with the same name but a completely different
functionality. This can make it difficult to trace the image back to the
build that generated it.

To **prevent tags from being overwritten**, you can configure a
repository to be immutable in the DTR web UI. Once configured, DTR will
not allow anyone else to push another image tag with the same name.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 60: c**

*Explanation*

The main purpose of a CMD is to provide defaults for an executing
container. These defaults can include an executable, or they can omit
the executable, in which case you must specify an ENTRYPOINT instruction
as well.

If CMD is used to provide default arguments for the ENTRYPOINT
instruction, both the CMD and ENTRYPOINT instructions should be
specified with the JSON array format.

[[https://docs.docker.com/engine/reference/builder/\#cmd]{.ul}](https://docs.docker.com/engine/reference/builder/#cmd)

### **Answer 61: b**

*Explanation*

The WORKDIR instruction sets the working directory for any RUN, CMD,
ENTRYPOINT, COPY and ADD instructions that follow it in the Dockerfile.
If the WORKDIR doesn't exist, it will be created even if it's not used
in any subsequent Dockerfile instruction.

[[https://docs.docker.com/engine/reference/builder/\#workdir]{.ul}](https://docs.docker.com/engine/reference/builder/#workdir)

### **Answer 62: a**

*Explanation*

An ENTRYPOINT allows you to configure a container that will run as an
executable.

You can override the ENTRYPOINT instruction using the docker run
\--entrypoint flag.

[[https://docs.docker.com/engine/reference/builder/\#entrypoint]{.ul}](https://docs.docker.com/engine/reference/builder/#entrypoint)

The main purpose of a CMD is to provide defaults for an executing
container. These defaults can include an executable, or they can omit
the executable, in which case you must specify an ENTRYPOINT instruction
as well.

If CMD is used to provide default arguments for the ENTRYPOINT
instruction, both the CMD and ENTRYPOINT instructions should be
specified with the JSON array format.

The CMD instruction has three forms:

· CMD \[\"executable\",\"param1\",\"param2\"\] (exec form, this is the
preferred form)

· CMD \[\"param1\",\"param2\"\] (as default parameters to ENTRYPOINT)

· CMD command param1 param2 (shell form)

[[https://docs.docker.com/engine/reference/builder/\#cmd]{.ul}](https://docs.docker.com/engine/reference/builder/#cmd)

### **Answer 63: b**

*Explanation*

**Delete signed images**

DTR only allows deleting images if the image has not been signed. You
first need to delete all the trust data associated with the image before
you are able to delete the image.

[[https://github.com/docker/docker.github.io]{.ul}](https://github.com/docker/docker.github.io)

### **Answer 64: b**

*Explanation*

Docker builds images automatically by reading the instructions from a
Dockerfile text file that contains all commands, in order, needed to
build a given image.

A Docker image consists of read-only layers each of which represents a
Dockerfile instruction.

[[https://docs.docker.com/develop/develop-images/dockerfile_best-practices/]{.ul}](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

### **Answer 69: d**

*Explanation*

**Best practices for writing Dockerfiles:**

· Create ephemeral containers

· Understand build context

· Pipe Dockerfile through stdin

· Exclude with .dockerignore

· Use multi-stage builds

· Don't install unnecessary packages

· Decouple applications

· Minimize the number of layers

· Sort multi-line arguments

· Leverage build cache

[[https://docs.docker.com/develop/develop-images/dockerfile_best-practices/\#create-ephemeral-containers]{.ul}](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#create-ephemeral-containers)

### **Answer 66: c**

*Explanation*

Multi-stage builds allow you to drastically reduce the size of your
final image, without struggling to reduce the number of intermediate
layers and files.

[[https://docs.docker.com/develop/develop-images/dockerfile_best-practices/\#use-multi-stage-builds]{.ul}](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#use-multi-stage-builds)

With multi-stage builds, you use multiple FROM statements in your
Dockerfile. Each FROM instruction can use a different base, and each of
them begins a new stage of the build. You can selectively copy artifacts
from one stage to another, leaving behind everything you don't want in
the final image.

[[https://docs.docker.com/develop/develop-images/multistage-build/\#use-multi-stage-builds]{.ul}](https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds)

### **Answer 67: a**

*Explanation*

    VOLUME ["/data"]

The VOLUME instruction creates a mount point with the specified name and
marks it as holding externally mounted volumes from native host or other
containers. The value can be a JSON array, VOLUME \[\"/var/log/\"\], or
a plain string with multiple arguments, such as VOLUME /var/log or
VOLUME /var/log /var/db.

[[https://docs.docker.com/engine/reference/builder/\#volume]{.ul}](https://docs.docker.com/engine/reference/builder/#volume)

### **Answer 68: a**

*Explanation*

In an image, a layer is modification to the image, represented by an
instruction in the Dockerfile. Layers are applied in sequence to the
base image to create the final image.

When an image is updated or rebuilt, only layers that change need to be
updated, and unchanged layers are cached locally. This is part of why
Docker images are so fast and lightweight. The sizes of each layer add
up to equal the size of the final image.

[[https://docs.docker.com/glossary/]{.ul}](https://docs.docker.com/glossary/)

### **Answer 69: d**

*Explanation*

Docker Hub is a service provided by Docker for finding and sharing
container images with your team. It provides the following major
features:

· Repositories: Push and pull container images.

· Teams & Organizations: Manage access to private repositories of
container images.

· Official Images: Pull and use high-quality container images provided
by Docker.

· Publisher Images: Pull and use high-quality container images provided
by external vendors. Certified images also include support and guarantee
compatibility with Docker Enterprise.

· Builds: Automatically build container images from GitHub and Bitbucket
and push them to Docker Hub.

· Webhooks: Trigger actions after a successful push to a repository to
integrate Docker Hub with other services.

[[https://docs.docker.com/docker-hub/]{.ul}](https://docs.docker.com/docker-hub/)
