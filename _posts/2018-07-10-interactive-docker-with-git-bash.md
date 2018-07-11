---
layout: post
title: "Interactive Docker Container with Git-Bash and Winpty"
description: "Half past three in the morning - Problem solved!"
date: 2018-07-10
---

Yeah man. Since I use Docker on Windows 10 I had problems to run some <code>docker run</code>
commands on Git-Bash. Today I finally figured out that the problems applies only to those
Docker run commands with both <code>--interactive</code> and <code>--tty</code>
(or simply <code>-it</code>) options together in combination with directory paths.

To run a Docker container with interactive mode and pseudo-TTY I have to use Winpty.

~~~ shell
docker run --rm -it alpine sh
# Output
the input device is not a TTY.  If you are using mintty, try prefixing the command with 'winpty'
~~~

~~~ shell
winpty docker run --rm -it alpine sh
# Output
/ $
~~~

That was easy. But if I am going to mount the current directory on container startup I get
an error.

~~~ shell
winpty docker run --rm -it -v $PWD:/mnt alpine sh
# Output
C:/Program Files/Docker/Docker/Resources/bin/docker.exe: Error response from daemon: Mount denied:
The source path "C:/Users/Thomas/Workspaces;C"
doesn't exist and is not known to Docker.
See 'C:/Program Files/Docker/Docker/Resources/bin/docker.exe run --help'.
~~~

Also when I try something like <code>ls /usr</code> on a container I get an error.

~~~ shell
winpty docker run --rm -it alpine ls /usr
# Output
ls: C:/Program Files/Git/usr: No such file or directory
~~~

It seems that Docker gets wrong paths from Winpty.

I have found several suggestions how to handle this. But only one is acceptable for me
and this is to execute <code>exec winpty bash</code> before I start my Docker session.
After this I can run all Docker commands without to prefix with Winpty without problems.

~~~ shell
export MSYS_NO_PATHCONV=1
exec winpty bash
docker run --rm -it -v $PWD:/mnt alpine sh
# Output
/ $
~~~

I do not know why <code>exec winpty bash</code> solves this problem. And I do not know
if this has any impact for other programs but for now I am happy that I have found this
solution randomly on this [comment](https://github.com/docker/toolbox/issues/323#issuecomment-376276636).
