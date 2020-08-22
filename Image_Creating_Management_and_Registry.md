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
