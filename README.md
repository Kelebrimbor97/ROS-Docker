# ROS-Docker

### Description

Working with robotics involves using many different software suites that can often clash with each other. In Python projects, environments like Anaconda or virtual enviroments are commonly used to manage dependencies. However, ROS installations can be tedious and are often prone to breaking. Therefore, using Docker containers is often a better option than relying on a base installation, as they provide a more stable and isolated environment.


## 1. Instructions to have a stable Ubuntu installation
>[!Warning]
>- Skip following instructions in this section if you plan to use any other OS except Ubuntu 22.04 or Ubuntu 20.04. Note that running a docker container is independent of this.
>- This section is for Computer with a **Nvidia GPU ONLY**. People with other GPUs should skip this section.

For any of your projects, having a stable Ubuntu Installation is of foremeost importance as the main image installed in you computer provides a stable foundation for everything else, be it a conda environment or as it is in this case, a Docker Image.

For this course, and for a stable installation, we recommend that you install either [Ubuntu 20.04](https://releases.ubuntu.com/focal/) or [Ubuntu 22.04](https://releases.ubuntu.com/jammy/).


>[!Note]
> Although as of the moment this tutorial is being written, Ubuntu has been out for around 4 months, it doesn't support Lambda stack yet, which we use to have a super stable installation that makes sure that you don't have to deal with driver issues.


>[!Important]
> Remember to be equipped with the following things before you get started with the installation:
> 1. A computer with an Ubuntu 22.04 or 20.04 installation (prefereable fresh but not important).
> 2. A stable and high - speed internet connection
> 3. High patience. At times, the downloads may be slow regardless of how fast your connection is. It may be just an hour or as long as 6 to 8.
> 4. Habit of periodically checking in.

After you are done installing Ubuntu, follow the following instructions from Lambda Labs to install the [Lambda stack](https://lambdalabs.com/lambda-stack-deep-learning-software)


1. Run the first command:

    `wget -nv -O- https://lambdalabs.com/install-lambda-stack.sh | sh -`

2. Once it is done, proceed to reboot by doing:

    `sudo reboot`

3. Now, proceed to update everything to the latest installation

    `sudo apt-get update && sudo apt-get dist-upgrade`

> [!Note]
>- It is a good practice to regularly update your system using:
> `sudo apt-get update && sudo apt-get upgrade`
>- followed by:
> `sudo apt-get dist-upgrade`

4. We now utilize a GPU accelerated docker using the following command:

    `sudo apt-get install docker.io nvidia-container-toolkit`

And that's it, you have a very stable installation that includes PyTorch®, TensorFlow, CUDA, cuDNN, and NVIDIA Drivers!

## 2. Docker Setup (Ubuntu Only)

Now that you have all the prerequisites installed with Ubuntu, we can get started with Docker. Note that we are installing only Docker Engine, and not Docker Desktop.

([Official Instructions to install Docker Engine](https://docs.docker.com/engine/install/ubuntu/))

> [!Note]
>- Since we support only Ubuntu installations for this course, the **following steps are for Ubuntu ONLY**.
>- Follow the steps from official documentation, if you wish to use Docker Desktop for [Windows](https://docs.docker.com/desktop/install/windows-install/) or [MacOS](https://docs.docker.com/desktop/install/mac-install/).

### 2.1 Installing Docker Engine

> [!Caution]
> Skip this sub-section and move directly to sub-section 2.2 if you followed section 1 

1. Uninstall old packages:

    `for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done`

2. Install Docker Engine using Docker's `apt` repository, by running the sequence of commands below. They are in bullets to avoid confusion.
    
    - `sudo apt-get update`
    
    - `sudo apt-get install ca-certificates curl`
    
    - `sudo install -m 0755 -d /etc/apt/keyrings`

    - `sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc`

    - `sudo chmod a+r /etc/apt/keyrings/docker.asc`
    
    - ```echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null```
    
    - `sudo apt-get update`

3. Install the Docker Packages:

    `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`

4. Verify that the Docker Engine installation is successful by running the `hello-world` image:

    `sudo docker run hello-world`

### 2.2 Post Installation steps

After installation, for Ubuntu based installation, you must run the following commands:

1. `sudo groupadd docker`
2. `sudo usermod -aG docker $USER`

Now, reboot your system with:

3. `sudo reboot`

Login again and run the following command:

4. `newgrp docker`

Finally, to verify that we can run `docker` without `sudo`, run the `hello-world` container using the command:

5. `docker run hello-world`

If it runs, you have successfully run the post-installation steps.

## 3. Setting up the ROS environment

We are finally ready to use our ROS Docker image. To do that, clone this repo, build the docker image, and run it using the following steps:

### 3.1. Install git:
    
`sudo apt-get install git`

### 3.2. Running the Docker:

1. Clone this repository using the command:

    `git clone https://github.com/Kelebrimbor97/ROS-Docker.git`

>[!TIP]
> Remeber to do a `git pull` from within your repo to update your repo to the latest versions.

3. Navigate to to location where the Dockerfile is stored:

    `cd ROS-Docker/Scripts/Galactic/`

4. Build the docker Image using this command:

> [!IMPORTANT]
> Take a look at the comments on lines 9 and 10 of the  in `Scripts/Galactic/Dockerfile` before you run this command.

    docker build -t modelling_ros .

> [!TIP]
>- `modelling_ros` can be replaced with any other name of your choice, but remember to replace it in future Dockerfiles you create.

> [!NOTE]
>- The following 2 commands are what you have to use everytime you want to run the docker.

4. Allow docker to have port access:

    `xhost +local:docker`

5. Spin up a container by using the image created in the previous step:

    `docker run -it --rm --name=project_0 --gpus=all --net=host --pid=host --privileged --env="DISPLAY=$DISPLAY" modelling_ros`

> [!TIP]
>- You can again have a container name of you choice instead of `project_0`.

6. It's Alive! If you see something like this, your docker container is up and running:

    `root@User:/#  `

    If not, feel free to cry...

### 3.3. Execing into the Docker (Opening a separate terminal in same container)

>[!Warning]
>- Any changes you make to the docker container will not be saved and will be lost once the current container is shut down.

Once you have a container running, start using it as you would with a terminal. The only difference is that you never need to use `sudo` again.

For opening a different terminal in the same container, get the container name and `exec` into it. Example:

`docker exec -it project_0 bash`

## 4. Installing turtlebot3

You can try installing turtlebot3 using the following instructions inside your running Docker container.
