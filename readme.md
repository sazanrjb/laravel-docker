Docker is a container technology which allows shipping developing and shipping application along with all the parts that it needs.

Here are few things required for a Dockerfile:

**FROM**
- Specify the base image to be used for this container
```
FROM alpine-php
```

**MAINTAINER**
- Author or Owner of this container
- `Name <Email>`

```
MAINTAINER Sajan Rajbhandari <sazanrjb@gmail.com>
```
---

**RUN**
- Similar to running bash, and interactively running commands
- There can be multiple RUN commands
- Executes at build time
- Used to install apps

```
RUN apt-get update
```
---

**CMD**
- Similar to RUN
- Executes at run time
- Runs commands in container at lunch time
- There can only be one CMD in a Dockerfile
- It has two styles of syntax i.e. Shell form and Exec form
- Shell form
     - Expressed the same way as shell commands
     - Commands get prepended by `/bin/sh -c`
     - Variables can be used
- Exec form
     - JSON array style `["command", "arg1"]`
     - Recommended
     - Containers don't need shell
     - Variables cannot be used
```
CMD echo "Hello"
```
---

**ENTRYPOINT**
- Preferred method of specifying default app to run inside a container
- Not compulsory
- Can't be overridden at run-time with normal commands - docker run <command>
- But can be override cmd commands with this
- Any command at run-time is used as an argument to ENTRYPOINT
```
ENTRYPOINT ["echo"]
```
- `docker run CONTAINER_NAME Hello`
    - Hello is passed as an argument
    - CMD instructions in dockerfile is overridden if argument is passed in docker run command
---

**ENV**
- Create environment variables
```
ENV var1=Kathmandu var2=Nepal
```
- Can be used in CMD like CMD $var1 $var2
---

**VOLUME**
- Decoupling data from containers
- Sharing data between containers
- Specify directory or mount point within a container and store data into that location
- If container is stopped or deleted, data persists
```
docker run -it -v /test-vol --name=volumn1 CONTAINER_NAME /bin/bash
VOLUME /data
```
- To remove: `docker rm -v CONTAINER_NAME`



