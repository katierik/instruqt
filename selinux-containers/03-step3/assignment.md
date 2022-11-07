---
slug: step3
id: p32zmlmedrlm
type: challenge
title: Generating SELinux container policies with Udica
tabs:
- title: Terminal
  type: terminal
  hostname: rhel
difficulty: basic
timelimit: 1
---
To create the custom SELinux security policy, Udica scans the container JSON
file to discover which Linux capabilities are required by the container. The
network ports are a similar situation where Udica uses the SELinux userspace
libraries to get the correct SELinux label of a port that is used by the
inspected container.

In 'Pane 0' of the lab interface, inspect the running container using
podman to generate a container inspection file in JSON format

```bash
podman inspect $CONTAINERID > container.json
```

Tell Udica to generate the custom SELinux security policy by using the container
JSON file. In this case the name of the custom SELinux security policy is called
'my_container'

```bash
udica -j container.json my_container
```

<pre class="file">

Policy my_container created!

Please load these modules using:
\# semodule -i my_container.cil /usr/share/udica/templates/{base_container.cil,net_container.cil,home_container.cil}

Restart the container with: "--security-opt label=type:my_container.process" parameter
</pre>

You just created a custom SELinux security policy for the container. Now you can
load this policy into the kernel and make it active.

```bash
semodule -i my_container.cil /usr/share/udica/templates/{base_container.cil,net_container.cil,home_container.cil}
```

For the policies to take effect, stop and re-launch the container

```bash
podman stop $CONTAINERID
```

In 'Pane 1' tab of the lab interface, create a new container runtime from
the image which uses the new, custom container policy

```bash
CONTAINER=$(podman run --security-opt label=type:my_container.process -v /home:/home:ro -v/var/spool:/var/spool:rw -d -p 80:80 -it registry.access.redhat.com/ubi9/ubi)
```
