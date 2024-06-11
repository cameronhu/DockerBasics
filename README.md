# DockerBasics
Repo to learn Docker and containers

Reference Tutorials:

https://www.youtube.com/watch?v=iqqDU2crIEQ&t=1002s

https://www.youtube.com/watch?v=pg19Z8LL06w&t=2348s

**Docker** is software for building **containers**, which is an advancement on virtual environment and virtual machines that allows you to package applications with all of its dependencies so that it can be shipped to different machines or servers and work straight out of the box. Containers contain

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fe052c67-27af-4b39-953c-2186f352e147/d9fc6977-4078-4159-a4a5-5ee67381d1fb/Untitled.png)

Originally, applications were developed directly on specific operating systems, which created numerous issues. For example, some applications would dominate hardware resources, causing other applications to underperform. Additionally, because applications were developed for particular OSes and under specific package dependencies and runtime conditions, troubleshooting applications for deployment on other systems was challenging. To address these issues, Virtual Machines (VMs) were designed to encapsulate an entire operating system on top of the base hardware and OS of the machine. Not only this, VMs virtualize base hardware components such as memory, CPU, etc. This allowed applications to run in isolated environments within their own VMs. However, VMs are relatively bulky due to their scope of encapsulation. This led to the development of Containers, Docker, and containerized development, which offer a more lightweight solution.

A side note: **Virtual Environments** are another variation on virtual encapsulation. Instead of virtualizing the whole machine, the base OS is used; isolating the different package dependencies of an application are the focus of venvs, given that certain applications require specific versions of Python or other packages. 

The way Docker functions is through **Docker Images**, which are defined by **Dockerfiles**. Dockerfiles contains instructions, in Docker syntax, for what dependencies the application needs, such as the Python version, various libraries, etc. This is quite useful as different systems will have different compute environments, and Docker solves this problem! In our case, it is useful for connecting to our HPC environment, RCE2.

Docker works by starting off base image layers, and then adding layers on top of it to have the final environment required. 

To start off with a common base image, go to [`hub.docker.com`](http://hub.docker.com) and search up a base image, such as Miniconda. Can pull from that base image using the command found there, and then Jonathan suggests using that base image’s pre-installed `pip` to pip install other python packages.

To build a docker image, use the following command:

`docker build -t test:latest .` 

which finds the Dockerfile and any files listed in the Dockerfile required to build the image in the current directory, via the last `.` in the command.

Once the Docker Image is built, one needs to run the Image by starting up a **Container,** which can be done by using the `docker run` command.

When using multiple `FROM` statements in a Dockerfile, you are building multiple layers upon which the image is constructed. However, only the final layer, or the commands in the final `FROM` block are actually built into the image, the previous `FROM` blocks are just intermediaries, according to Copilot. Therefore, even with multiple `FROM` layers, you will only have one final image after building, which will only have the dependencies listed in the final block when you spin up the container.
