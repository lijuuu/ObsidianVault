

---

## Table of Contents 📋
- [Installation and Setup 🔧](#installation-and-setup-)
- [Container Management 🐳](#container-management-)
- [Image Management 🖼️](#image-management-)
- [Networking 🌐](#networking)
- [Volumes 💾](#volumes-)
- [System Management 🛠️](#system-management-)
- [Docker Compose 📜](#docker-compose-)
- [Plugins 🔌](#plugins-)
- [Context Management 🌍](#context-management-)
- [SBOM Generation 📊](#sbom-generation-)
- [Tips and Best Practices 💡](#tips-and-best-practices-)

---

## Installation and Setup 🔧
Get Docker up and running! 🚀

- **Check Docker Version**  
  `docker --version`  
  📌 Displays the Docker CLI and daemon version.  

- **Get System Info**  
  `docker info`  
  📌 Shows detailed info about the Docker environment (e.g., containers, images, plugins).  

- **Install Docker (Ubuntu Example)**  
  `sudo apt-get update && sudo apt-get install docker.io`  
  📌 Adjust for your OS (e.g., `yum` for CentOS, Docker Desktop for Windows/Mac).  

---

## Container Management 🐳
Manage your containers like a pro! 🏆

- **List Running Containers**  
  `docker ps`  
  📌 Add `-a` to see all containers (including stopped ones).  

- **Run a Container**  
  `docker run [OPTIONS] IMAGE [COMMAND]`  
  - `-d`: Run in detached mode.  
  - `-i`: Interactive mode (keep STDIN open).  
  - `-t`: Allocate a pseudo-TTY.  
  - `--name NAME`: Name the container.  
  - `-p HOST_PORT:CONTAINER_PORT`: Map ports.  
  - `-v HOST_DIR:CONTAINER_DIR`: Mount a volume.  
  - `-e KEY=VALUE`: Set environment variables.  
  Example: `docker run -d -p 8080:80 nginx`  

- **Start a Container**  
  `docker start CONTAINER_ID_OR_NAME`  
  📌 Starts a stopped container.  

- **Stop a Container**  
  `docker stop CONTAINER_ID_OR_NAME`  
  📌 Stops a running container gracefully.  

- **Restart a Container**  
  `docker restart CONTAINER_ID_OR_NAME`  
  📌 Restarts a container.  

- **Kill a Container**  
  `docker kill CONTAINER_ID_OR_NAME`  
  📌 Forces a container to stop.  

- **Remove a Container**  
  `docker rm CONTAINER_ID_OR_NAME`  
  📌 Deletes a stopped container. Add `-f` to force removal of running containers.  

- **Execute Command in Running Container**  
  `docker exec [OPTIONS] CONTAINER COMMAND`  
  - `-i`: Interactive.  
  - `-t`: TTY.  
  Example: `docker exec -it mycontainer /bin/bash`  

- **Inspect Container Details**  
  `docker inspect CONTAINER_ID_OR_NAME`  
  📌 Shows detailed metadata (e.g., IP address, network settings).  

- **View Container Logs**  
  `docker logs CONTAINER_ID_OR_NAME`  
  📌 Add `-f` to follow logs in real-time.  

- **Rename a Container**  
  `docker rename OLD_NAME NEW_NAME`  
  📌 Renames a container.  

- **Copy Files To/From Container**  
  `docker cp [HOST_PATH] CONTAINER:CONTAINER_PATH`  
  `docker cp CONTAINER:CONTAINER_PATH [HOST_PATH]`  
  Example: `docker cp ./file.txt mycontainer:/app`  

---

## Image Management 🖼️
Work with Docker images efficiently! 🎨

- **List Images**  
  `docker images`  
  📌 Add `-a` to include intermediate images.  

- **Pull an Image**  
  `docker pull IMAGE[:TAG]`  
  Example: `docker pull ubuntu:latest`  

- **Build an Image**  
  `docker build [OPTIONS] PATH`  
  - `-t NAME:TAG`: Tag the image.  
  - `-f PATH/DOCKERFILE`: Specify Dockerfile.  
  Example: `docker build -t myapp:1.0 .`  

- **Tag an Image**  
  `docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`  
  Example: `docker tag myapp:1.0 myregistry/myapp:1.0`  

- **Push an Image**  
  `docker push IMAGE[:TAG]`  
  📌 Push to a registry (e.g., Docker Hub) after logging in with `docker login`.  

- **Remove an Image**  
  `docker rmi IMAGE_ID_OR_NAME`  
  📌 Deletes an image. Add `-f` to force removal.  

- **Save Image to Tar Archive**  
  `docker save -o FILENAME.tar IMAGE`  
  Example: `docker save -o myimage.tar myapp:1.0`  

- **Load Image from Tar Archive**  
  `docker load -i FILENAME.tar`  
  📌 Loads an image from a tar file.  

- **Export Container Filesystem**  
  `docker export -o FILENAME.tar CONTAINER`  
  📌 Exports a container’s filesystem as a tar archive.  

- **Import Tarball as Image**  
  `docker import FILENAME.tar REPO:TAG`  
  📌 Creates an image from a tarball.  

- **Show Image History**  
  `docker history IMAGE`  
  📌 Displays the build history of an image.  

---

## Networking 🌐
Connect your containers seamlessly! 🔗

- **List Networks**  
  `docker network ls`  
  📌 Shows all networks (e.g., bridge, host, none).  

- **Create a Network**  
  `docker network create NETWORK_NAME`  
  Example: `docker network create mynetwork`  

- **Inspect a Network**  
  `docker network inspect NETWORK_NAME`  
  📌 Details about a network (e.g., connected containers).  

- **Connect Container to Network**  
  `docker network connect NETWORK_NAME CONTAINER`  
  📌 Connects a running container to a network.  

- **Disconnect Container from Network**  
  `docker network disconnect NETWORK_NAME CONTAINER`  
  📌 Disconnects a container from a network.  

- **Remove a Network**  
  `docker network rm NETWORK_NAME`  
  📌 Deletes a network (if no containers are using it).  

---

## Volumes 💾
Manage data persistence like a boss! 📦

- **List Volumes**  
  `docker volume ls`  
  📌 Shows all volumes.  

- **Create a Volume**  
  `docker volume create VOLUME_NAME`  
  Example: `docker volume create myvolume`  

- **Inspect a Volume**  
  `docker volume inspect VOLUME_NAME`  
  📌 Details about a volume (e.g., mount point).  

- **Remove a Volume**  
  `docker volume rm VOLUME_NAME`  
  📌 Deletes a volume (if not in use).  

---

## System Management 🛠️
Keep your Docker environment clean! 🧹

- **Prune Unused Resources**  
  `docker system prune`  
  📌 Removes unused containers, networks, and images. Add `-a` to include all unused images.  

- **Check Disk Usage**  
  `docker system df`  
  📌 Shows disk usage by containers, images, and volumes.  

- **Remove Dangling Images**  
  `docker image prune`  
  📌 Deletes unused (dangling) images.  

- **Remove Stopped Containers**  
  `docker container prune`  
  📌 Deletes all stopped containers.  

- **Remove Unused Volumes**  
  `docker volume prune`  
  📌 Deletes unused volumes.  

- **Remove Unused Networks**  
  `docker network prune`  
  📌 Deletes unused networks.  

---

## Docker Compose 📜
Orchestrate multi-container apps! 🎼

- **Build and Start Services**  
  `docker compose up`  
  📌 Starts services defined in `docker-compose.yml`. Add `-d` for detached mode.  

- **Stop and Remove Services**  
  `docker compose down`  
  📌 Stops and removes containers, networks, and volumes.  

- **Build Services**  
  `docker compose build`  
  📌 Builds or rebuilds services.  

- **Start Existing Services**  
  `docker compose start`  
  📌 Starts existing containers.  

- **Stop Services**  
  `docker compose stop`  
  📌 Stops running services.  

- **View Logs**  
  `docker compose logs`  
  📌 Shows logs for all services.  

---

## Plugins 🔌
Extend Docker’s functionality! ⚡

- **List Plugins**  
  `docker plugin ls`  
  📌 Shows installed plugins.  

- **Install a Plugin**  
  `docker plugin install PLUGIN`  
  📌 Installs a plugin (e.g., `docker plugin install foo/bar`).  

- **Enable a Plugin**  
  `docker plugin enable PLUGIN`  
  📌 Enables a plugin.  

- **Disable a Plugin**  
  `docker plugin disable PLUGIN`  
  📌 Disables a plugin.  

- **Remove a Plugin**  
  `docker plugin rm PLUGIN`  
  📌 Removes a plugin.  

---

## Context Management 🌍
Manage multiple Docker hosts! 🖥️

- **List Contexts**  
  `docker context ls`  
  📌 Shows available contexts.  

- **Create a Context**  
  `docker context create CONTEXT_NAME --docker host=HOST`  
  Example: `docker context create mycontext --docker host=tcp://192.168.1.100:2376`  

- **Use a Context**  
  `docker context use CONTEXT_NAME`  
  📌 Switches to the specified context.  

- **Update a Context**  
  `docker context update CONTEXT_NAME`  
  📌 Modifies a context’s configuration.  

- **Remove a Context**  
  `docker context rm CONTEXT_NAME`  
  📌 Deletes a context.  

---

## SBOM Generation 📊
Generate Software Bill of Materials! 📜

- **Generate SBOM for an Image**  
  `docker sbom IMAGE`  
  📌 Creates an SBOM for the specified image.  

- **Scan Image with Severity Filter**  
  `docker scan IMAGE --severity LEVEL`  
  📌 Scans for vulnerabilities (e.g., `--severity high`).  

---

## Tips and Best Practices 💡
- **Security**: Run containers as non-root users (`USER` in Dockerfile) and use `--read-only` mounts. 🔒
- **Cleanup**: Regularly run `docker system prune -a` to free up space. 🗑️
- **Logging**: Use `docker logs -f` for real-time monitoring. 📡
- **Networking**: Prefer user-defined networks over the default bridge network for better isolation. 🌉
- **Compose**: Use `docker-compose.yml` for multi-container apps to simplify management. 📝

---

Happy Dockerizing! 🚢💪 Let me know if you need more commands or examples! 😄