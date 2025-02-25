# Application Architecture

When we work on any application, there are 3 main things:

1) **Frontend**: Angular/ReactJS/Vue.js, etc.
2) **Backend**: Java/.NET/Python/PHP
3) **Database**: Oracle, MySQL DB, SQL Server

---

# Application Tech Stack

Suppose we are using the following for the project:

- **Frontend**: ReactJS 18.2.0v
- **Backend**: Java 17v
- **Database**: MySQL 8.5v
- **Tomcat**: 9.0v

---

# Environment Setup To Run Our Application

When we work in an organization, there will be different teams: Development Team, DevOps Team, etc. Now, if the DevOps team needs to deploy the application, they need to set up the environment.

So, to set up and run our application, they will require to do the following steps:

1) Take one machine (Physical / Virtual)
2) Install ReactJS 18.2.0v
3) Install Java 17v
4) Install Tomcat Server 9.0v
5) Install MySQL DB Server 8.5v

So, DevOps need to perform these steps to set up the environment. But in real-time, there will be multiple environments.

---

# Application Environment

![Different Environment](Images/Different-Environment.PNG)


1) **Dev**: Developers will use this environment for development purposes.
2) **QA**: The testing team will use this environment for testing the application.
3) **UAT**: Clients or client-side users will use this environment for testing the application.
4) **PILOT**: This is also called the Pre-Production Environment.
5) **PROD**: Live Environment (End users will use this environment).

---

# Challenges in Deployment Process

1) Multiple Environment Setup
2) Setting Up All Required Dependencies (Software) on All Machines
3) Version Conflicts
4) Environment Maintenance
5) Environment Issues

To solve this problem, we need Docker.

---

# Docker

- It is free and open-source software.
- It is used for containerization.
  
Containerization means packaging our "Application Code + Required Dependencies" as a single unit for execution.

![Docker Image](Images/Docker-Image.PNG)

There will be application code and dependencies software. We will combine both and create one Docker Image.

If any environment (Dev, QA, UAT, etc.) needs to set up, they will simply pull the Docker Image, and a Docker Container will get created.

So, like this, we don’t need to worry about version conflicts and installation of software.

This concept is called **Containerization**.

If we use Docker in our project, we can run our project on any system without worrying about the underlying software.

---

# Docker Architecture

If we want to understand the working of Docker, then we need to understand the architecture of Docker.

![Docker Architecture](Images/Docker-architecture.PNG)


1) **Docker File**

   - It contains a set of instructions to build our Docker image.
   - The Docker file is used to specify what the dependencies are to run our application.

2) **Docker Image**

   - It is the package of code + dependencies.
   - Once our Docker file is created, we will build a Docker Image using the Docker file.

3) **Docker Registry**

   - Once the Docker Image is created, we can store that Docker Image in Docker Hub / Docker Registry.
   - This is also called a push operation.
   - We can store the Docker image in different repositories like Nexus repository, JFrog repository, AWS ECR, etc.

4) **Docker Container**

   - Once the Docker Image is created, we can pull/run the Docker image on any system.
   - When we pull/run the Docker image, it creates a Docker container on our system.

---

**NOTE:**  
If tomorrow we want to change the version of Java from Java 17v to Java 21v, then we can make changes in the app code and Docker file and create a new Docker image of that application.  
We don’t need to make changes in every environment.  
That’s the beauty of Docker.

We also need to install Docker on the system. If there are 10 systems, we need to install Docker on each system.  
We just need to follow a few steps:
- Install Docker
- Pull the Docker Image
- Download the Docker Image
- Run the Docker Image

![Docker VM](Images/Docker-VM.PNG)


In the above image, we can see that we have our own machine (i.e., system).  
In that machine, we have Windows OS.  
And we just need to install Docker Software (also known as Docker Engine).  
Once that's done, we need to pull and run Docker Images available in Docker Hub.  
Once we pull the Docker Image, it will create a Virtual Machine (also known as a Docker Container).  
If we pull multiple Docker Images, multiple Virtual Machines will get created.  
Containers are created based on virtualization.  
So, we don’t need to install any software on the host machine because Docker will take care of that in the Virtual Machine.

---

# Install Docker Desktop

Go to the official website of Docker and install the suitable version of Docker Desktop on your system.  
Also, install WSL using the command prompt.  
To install WSL, simply execute the below command:

```bash
wsl --install
```

Basically, it will create a Linux machine on your system.  
Once everything is done, restart your system.

---

# Commands for Docker

To check if Docker is installed on your system or not, execute the below command:

```bash
docker --version
```

You will see the below result, which means that Docker is installed and working on your system:

```bash
Docker version 27.4.0, build bde2b89
```

---

# Pull an Image from Docker Hub

To pull an image from Docker Hub, execute the following command:

```bash
docker pull <image-id / image-name>
```

### Examples:

```bash
docker pull hello-world
docker pull openjdk
```

---
# Check Docker Images in the System

To check the total images in your system, execute the following command:

```bash
docker images
```

You will get output similar to the following:

```plaintext
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    d715f14f9eca   3 weeks ago   20.4kB
openjdk       latest    9b448de897d2   2 years ago   727MB
```

# Pull a Specific Version of an Image

If the user wants to pull a specific version of an image (e.g., Java), execute the following command:

```bash
docker pull openjdk:18
```

This will download the `18` version of the `openjdk` image.

You will get output similar to the following:

```plaintext
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    d715f14f9eca   3 weeks ago   20.4kB
openjdk       18        9b448de897d2   2 years ago   727MB
openjdk       latest    9b448de897d2   2 years ago   727MB
```

---
# Check Running Containers

To check if any container is running in your system, execute the following command:

```bash
docker ps
```

### Example:

```bash
docker ps
```

Output:

```plaintext
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

If you execute only `docker ps`, it will show the containers that are currently running.

---
# Check All Containers (Running and Stopped)

To check if any container is running or stopped in your system, execute the following command:

```bash
docker ps -a
```

### Example:

```bash
docker ps -a
```

Output:

```plaintext
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
87113732a3b3   hello-world   "/hello"   6 minutes ago   Exited (0) 5 minutes ago             busy_lamarr
```

If you execute `docker ps -a`, it will show both running and stopped containers.

---

### To run the docker image, execute the command below:

```bash
docker run <image-id / image-name>
```
After we run the command `docker run <image-name>`, a container gets created.

#### Example:

```bash
docker run hello-world
Hello from Docker!
This message shows that your installation appears to be working correctly.

NOTE: Here this is simple hello-world image so it got execute and exited automatically.
But if we pull image of web-app then it will not get exit automatically.


If we dont have docker image avaliable in our local system and even if we execute 
	docker run hello-world
Then in that case docker will check if there is any hello-world image is present in local
if hello-world image is not present in local then it will download that image  and run that image.

```

---

# Remove/Delete Docker Image

To remove/delete a Docker image, execute the following command:

```bash
docker rmi <image-id / image-name>
```

### Example:

1. **Check available Docker images:**

```bash
docker images
```

Output:

```plaintext
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    d715f14f9eca   3 weeks ago   20.4kB
openjdk       latest    9b448de897d2   2 years ago   727MB
```

2. **Delete Docker image by image name:**

```bash
docker rmi hello-world
```

Output:

```plaintext
Untagged: hello-world:latest
Deleted: sha256:d715f14f9eca81473d9112df50457893aa4d099adeb4729f679006bf5ea12407
```

3. **Verify deletion:**

```bash
docker images
```

Output:

```plaintext
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
openjdk      latest    9b448de897d2   2 years ago   727MB
```

4. **Delete Docker image by image ID:**

```bash
docker rmi 9b448de897d2
```

Output:

```plaintext
Untagged: openjdk:latest
Deleted: sha256:9b448de897d211c9e0ec635a485650aed6e28d4eca1efbc34940560a480b3f1f
```

5. **Verify all Docker images are deleted:**

```bash
docker images
```

Output:

```plaintext
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

---

## To remove/delete docker container execute below command

```bash
	docker rm	<container-id>
```

When you execute docker ps -a you will get the id of the container id

### Eg:	

## Checking if container is avaliable
```bash
 docker ps -a
```
Output:

```plaintext
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
87113732a3b3   hello-world   "/hello"   6 minutes ago   Exited (0) 5 minutes ago             busy_lamarr
```

## Deleted the container
```bash
docker rm 87113732a3b3
```
Output:

```plaintext
87113732a3b3
```

## Container got deleted
```bash
docker ps -a
```

Output:

```plaintext
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

---

## To delete stoped container and unused images execute below command
```bash
docker system prune -a
```

---
