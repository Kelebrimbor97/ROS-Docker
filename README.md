# ROS-Docker



## 1. Instructions to have a stable Ubuntu installation

For any of your projects, having a stable Ubuntu Installation is of foremeost importance as the main image installed in you computer provides a stable foundation for everything else, be it a conda environment or as it is in this case, a Docker Image.

For this course, and for a stable installation, we recommend that you install either [Ubuntu 20.04](https://releases.ubuntu.com/focal/) or [Ubuntu 22.04](https://releases.ubuntu.com/jammy/).


>[!Note]
> Although as of the moment this tutorial is being written, Ubuntu has been out for around 4 months, it doesn't support Lambda stack yet, which we use to have a super stable installation that makes sure that you don't have to deal with driver issues.

>[!Warning]
> Skip following instructions in this section if you plan to use any other OS except Ubuntu 22.04 or Ubuntu 20.04. Note that running a docker container is independent of this.

>[!Caution]
> Remeber to be equipped with the foloowing things before you get started with the installation:
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

> followed by:

> `sudo apt-get dist-upgrade`