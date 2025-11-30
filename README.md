# 🐳 Docker Guide   

## 📋 Table of Contents
- [Dockerfile](#dockerfile)
- [Docker Commands](#docker-commands)
- [Persistent Data and Volume Management](#persistent-data-and-volume-management)
- [Connecting Containers](#connecting-containers)
- [Docker Networking](#docker-networking)
- [Pro Tips](#pro-tips)
- [Important Links](#important-links)

## 🏗️ Dockerfile


FROM node  
WORKDIR /myapp  
COPY . /myapp/  
RUN npm install  
EXPOSE 3000  
CMD ["npm", "start"]  


## 🛠️ Docker Commands

### Create a Docker Image

docker build -t <image-name> .


### Check Docker Images

docker images
# OR
docker images ls


### Run the Image Inside a Container

docker run <image-id>


### Check Running Containers

docker ps


### Bind Container Port to Host Port

docker run -p 3000:3000 <image-id>


### Run Docker Image in the Background

docker run -d -p 3000:3000 <image-id>


### Run Multiple Containers from One Image

docker run -d -p 3001:3000 <image-id>
docker run -d -p 3002:3000 <image-id>
docker run -d -p 3004:3000 <image-id>


### View All Containers (Running and Stopped)

docker ps -a


### Delete a Container

docker rm <container-name>


### Stop a Running Container

docker stop <container-name>


### Automatically Delete Container After Stopping

docker run -d --rm -p 3000:3000 <image-id>


### Name Containers and Images

# Assign a Name to a Container
docker run -d --rm --name "prabin" -p 3001:3000 <image-id>

# Tagging Images
docker build -t prabin:01 .
docker build -t prabin:02 .


### Predefined Images

# Use a Specific Node.js Version in Dockerfile
FROM node:latest  # Or specify a version: node:14



# Pull Other Images
docker pull python
docker pull nginx

# Run an NGINX Container
docker run -p 8000:80 nginx:latest
# Access via: http://localhost:8000


## 💾 Persistent Data and Volume Management

### Save Data with Volumes

docker run -it --rm -v myvolume:/myapp <image-id>

- `-v` indicates volume usage.
- `myvolume` is the volume name.
- `/myapp` is the working directory in the Docker container.

### Check Volumes

docker volume ls


### Inspect Volume Details

docker volume inspect myvolume


### Mounting Local Files to Container

# Mount a File
docker run -it -v /path/to/local/file:/container/path -rm <image-id>

# Example:
docker run -it -v /User/root/Documents/pythonfilecontainer/requirement.txt:/myapp/requirement.txt -rm <image-id>


## 🔗 Connecting Containers

### Connecting Two Containers (e.g., Python and MySQL)

# Run a MySQL Container
docker pull mysql:latest
docker run -d --name mysqldb -e MYSQL_ROOT_PASSWORD="root" -e MYSQL_DATABASE="userinfo" mysql

# Inspect MySQL Container for IP Address
docker inspect mysqldb


Use the IP address (e.g., 172.17.0.2) to connect in your Python code:


host = "172.17.0.2"
user = "root"
password = "root"
database = "userinfo"


### Local MySQL and Python Code in Containers
Use `host.docker.internal` as the MySQL host:


host = "host.docker.internal"
user = "root"
password = "root"
database = "userinfo"


## 🌐 Docker Networking

### Create a Docker Network

docker network create my-net


### Run a MySQL Container on the Network

docker run -d --env MYSQL_DATABASE="userinfo" --env MYSQL_ROOT_PASSWORD="root" --name mysqldb --network my-net mysql


### Update Python Code to Use MySQL Container Name as Host

host = "mysqldb"
user = "root"
password = "root"
database = "userinfo"


## 💡 Pro Tips
- Always use specific versions for base images in production Dockerfiles.
- Use multi-stage builds to keep your final image size small.
- Leverage Docker Compose for managing multi-container applications.
- Regularly prune unused Docker objects to save disk space.

## 🔗 Important Links
- [Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

Happy Dockerizing! 🐳✨


These commands enhance your Docker workflow with:
- Image versioning and portability
- Container debugging
- System maintenance
- Resource management
- Network configuration
- Volume handling
- Service orchestration
- Monitoring capabilities

Each command is production-ready and commonly used in real-world scenarios.
