# Useful Commands

This README contains commands that I find useful, particularly on **UNIX-like** operating systems.

## Table of Contents

* [Conda](#conda)
* [Docker](#docker)
* [Git](#git)
* [Python](#python)
* [System Resources](#system-resources)
* [Miscellaneous](#miscellaneous)

## Conda

### Create virtual environment

```bash
conda create -n <env_name> [<package>...] [-y]
```

`<package>...`: List of packages to install in the environment.

`-y`: Answer "yes" to any confirmations automatically.

Example:

```bash
conda create -n ml python=3.9 numpy -y
```

### Enter virtual environment

```bash
conda activate <env_name>
```

Example:

```bash
conda activate ml
```

### Exit virtual environment

```bash
conda deactivate <env_name>
```

Example:

```bash
conda deactivate ml
```

### Clear `conda` cache

```bash
conda clean -a
```

## Docker

### Show all images

```bash
docker images
```

### Show all containers

```bash
docker ps -a [--size]
```

`--size`: Show size of each container.

### Pull image

```bash
docker pull <image_name>:<tag>
```

Example:

```bash
docker pull nvidia/cuda:11.8.0-devel-ubuntu22.04
```

### Create container

```bash
docker run [--gpus all] [-p <host_port>:<container_port>] [-v <host_dir>:<container_dir>] -it --name <container_name> <image_name>:<tag>
```

`--gpus all`: Access all available GPUs.

`-p <host_port>:<container_port>`: Map a port on the container to that on the host.

`-v <host_dir>:<container_dir>`: Mount a directory on the host inside the container.

Example:

```bash
docker run -it --name deeplearning nvidia/cuda:11.8.0-devel-ubuntu22.04
```

### Attach to running container

```bash
docker attach <container_name_or_id>
```

Example:

```bash
docker attach deeplearning
```

### Exit container

```bash
docker {stop, kill} <container_name_or_id>
```

`stop`: Exit gracefully.

`kill`: Exit immediately.

Example:

```bash
docker stop deeplearning
```

### Restart exited container

```bash
docker start <container_name_or_id>
```

Example:

```bash
docker start deeplearning
```

### Copy files to container

```bash
docker cp <local_source> <container_name_or_id>:<container_destination>
```

Example:

```bash
docker cp ./training_scripts/ deeplearning:/
```

### Copy files from container

```bash
docker cp <container_name_or_id>:<container_source> <local_destination>
```

Example:

```bash
docker cp deeplearning:/models/model_final.pth ./models/
```

### Start new process inside container

```bash
docker exec -it <container_name_or_id> <command>
```

Example:

```bash
docker exec -it deeplearning /bin/bash
```

### Remove container

```bash
docker rm <container_name_or_id>
```

Example:

```bash
docker rm deeplearning
```

### Build image from `Dockerfile`

```bash
docker build -t <tag> <path/to/Dockerfile>
```

Example:

```bash
docker build -t my-image .
```

### Save container as image

```bash
docker commit <container_name_or_id> <image_name>
```

### Export image as `.tar`

```bash
docker save -o <output_file>.tar <image_name>
```

### Load image from `.tar`

```bash
docker load -i <input_file>.tar
```

## Git

### Set commit email

```bash
git config [--global] user.email <email>
```

`--global`: Set commit email for every repository on the computer.

### Set commit username

```bash
git config [--global] user.name "<username>"
```

`--global`: Set commit username for every repository on the computer.

### Clone public repository

```bash
git clone {<repo_url>, <username>/<repo_name>}
```

### Clone private repository

```bash
git clone https://<pat>@github.com/<username>/<repo_name>.git
```

For more information on how to generate Personal Access Token (PAT), visit [How to clone a private repository from GitHub](https://www.educative.io/answers/how-to-clone-a-private-repository-from-github).

### Show uncommitted changes

```bash
git status
```

### Show differences

```bash
git diff
```

### Add changes to staging area

```bash
git add <file>...
```

Example:

```bash
git add .
```

### Restore files in working directory

```bash
git restore <file>...
```

### Commit changes to local repository

```bash
git commit -m "<message>"
```

### Push local changes to remote repository

```bash
git push
```

### Pull remote changes to local repository

```bash
git pull
```

## Python

### Install from public GitHub repository

```bash
python -m pip install git+https://github.com/<username>/<repo_name>.git[@<branch>]
```

`@<branch>`: Select desired branch.

Example:

```bash
python -m pip install git+https://github.com/anson416/python-utilities.git
```

### Install from private GitHub repository

```bash
python -m pip install git+https://<pat>@github.com/<username>/<repo_name>.git[@<branch>]
```

### Create `requirements.py`

```bash
python -m pip freeze > requirements.py
```

### Clear `pip` cache

```bash
python -m pip cache purge
```

## System Resources

### Show running processes

```bash
top
```

### Show info about CPU

```bash
lscpu
```

### Show info about memory

```bash
free -h
```

### Monitor CPU & memory

```bash
htop
```

### Monitor NVIDIA GPU

```bash
watch -n 1 nvidia-smi
```

### Show disk usage

```bash
df -h
```

### Show directory size

```bash
du -h <dir>
```

Example:

```bash
du -h datasets/
```

## Miscellaneous

### Download files

```bash
wget [-P <dir>] <urls>
```

_Note_: `-P`: Specify download directory, which defaults to `.` (i.e., current directory).

### Zip files

```bash
zip -r ./<zip_name>.zip <file>... [-x <exclude>...]
```
