## Task 1:

### Documentation Summary
Here’s a summary of what happens when you run an image that exists vs. does not exist locally:

| Scenario | What Happens? |
|----------|--------------|
| First time running `hello-world` | Docker pulls the image from Docker Hub, creates a container, and runs it. |
| Running it again | Docker does not pull the image again, but creates a new container from the existing image. |
| Listing images | `docker images` shows that the `hello-world` image now exists locally. |
| Listing all containers | `docker ps -a` shows the history of all previously run containers. |



## Task 2:

### Documentation Summary

| Step | Command | Explanation |
|------|---------|-------------|
| Download Nginx Image | `docker pull nginx` | Pulls the latest Nginx image from Docker Hub. |
| Run Nginx Container | `docker run -d -p 80:80 --name my-nginx nginx` | Runs Nginx in a container and exposes it on port 80. |
| Check Running Containers | `docker ps` | Lists running containers. |
| Verify in Browser | Open `http://localhost` | Confirms Nginx is running. |
| Stop Container | `docker stop my-nginx` | Stops the running container. |
| Remove Container (optional) | `docker rm my-nginx` | Deletes the container. |



## Task 3 :

### Documentation Summary

| Step | Command | Explanation |
|------|---------|-------------|
| Check running containers | `docker ps` | Lists active containers. |
| Try to remove running container | `docker rm my-nginx` | Fails because the container is running. |
| Force remove | `docker rm -f my-nginx` | Stops and deletes the container immediately. |
| Verify removal | `docker ps -a` | Confirms the container is gone. |


## Task 4:



| Step | Command | Explanation |
|------|---------|-------------|
| Run Nginx | `docker run -d -p 80:80 --name my-nginx nginx` | Starts Nginx container. |
| Check webpage | Open `http://localhost` | Confirms Nginx is running. |
| Access container shell | `docker exec -it my-nginx bash` | Opens a shell inside the container. |
| Fix TTY error | `winpty docker exec -it my-nginx bash` | Ensures compatibility in Git Bash. |
| Update system | `apt update && apt upgrade -y` | Updates package lists. |
| Fix `sudo` issue | `apt install sudo -y` | Installs `sudo` inside the container. |
| Locate HTML file | `cd /usr/share/nginx/html` | Finds the default Nginx index page. |
| Edit with `nano` | `nano index.html` | Modifies the homepage content. |
| Verify changes | Refresh `http://localhost` | Shows the updated homepage. |


## Task 5:

| Step | Command | Explanation |
|------|---------|-------------|
| Run second container on port 80 | `docker run -d -p 80:80 --name dreamteam-nginx daraymonsta/nginx-257:dreamteam` | Fails due to port conflict. |
| Check existing containers | `docker ps -a` | Lists all containers (running and stopped). |
| Remove failed container | `docker rm dreamteam-nginx` | Deletes the failed container. |
| Run container on port 90 | `docker run -d -p 90:80 --name dreamteam-nginx daraymonsta/nginx-257:dreamteam` | Maps container’s port 80 to host’s port 90. |
| Verify in browser | Open `http://localhost:90` | Confirms that the new container is running. |


## Task 6:
| Step | Command | Explanation |
|------|---------|-------------|
| Create an image | `docker commit my-nginx mrmri9/custom-nginx:v1` | Saves the running container as a Docker image. |
| Verify image | `docker images` | Lists all available images. |
| Log in to Docker Hub | `docker login` | Ensures access to push images. |
| Push image | `docker push mrmri9/custom-nginx:v1` | Uploads the custom image to Docker Hub. |
| Run container from Docker Hub | `docker run -d -p 8080:80 --name my-custom-nginx mrmri9/custom-nginx:v1` | Runs a container from the pushed image. |
| Verify container | `docker ps` | Checks if the container is running. |
| Test in browser | Open `http://localhost:8080` | Confirms that the new container is using the modified page. |


---

## Task 7: 
| Step | Command | Explanation |
|------|---------|-------------|
| Create project folder | `mkdir tech501-mod-nginx-dockerfile && cd tech501-mod-nginx-dockerfile` | Organizes project files. |
| Create `index.html` | `touch index.html` | Custom homepage for Nginx. |
| Create `Dockerfile` | `touch Dockerfile` | Automates Nginx customization. |
| Build the image | `docker build -t tech501-nginx-auto:v1 .` | Creates a custom Docker image. |
| Run the container | `docker run -d -p 8080:80 --name auto-nginx tech501-nginx-auto:v1` | Runs the modified Nginx container. |
| Tag the image | `docker tag tech501-nginx-auto:v1 mrmri9/nginx-auto:v1` | Prepares for Docker Hub push. |
| Push the image | `docker push mrmri9/nginx-auto:v1` | Uploads the image to Docker Hub. |
| Remove local image | `docker rmi tech501-nginx-auto:v1` | Deletes local copy. |
| Run from Docker Hub | `docker run -d -p 9191:80 --name fresh-nginx mrmri9/nginx-auto:v1` | Forces Docker to pull the image. |
| Verify running container | `docker ps` | Ensures the container is active. |
| Check in browser | Open `http://localhost:9191` | Confirms the image was pulled successfully. |

---

## Task 8:

| Step | Command | Explanation |
|------|---------|-------------|
| Create project folder | `mkdir sparta-node-docker && cd sparta-node-docker` | Organizes project files. |
| Copy `app` folder | `cp -r ~/onedrive/documents/github/app ./app` | Copies the app for containerization. |
| Create `Dockerfile` | `touch Dockerfile` | Defines the build process for the container. |
| Build the image | `docker build -t sparta-node:v1 .` | Creates the Docker image. |
| Run container locally | `docker run -d -p 3000:3000 --name sparta-node sparta-node:v1` | Runs the Node.js app in a container. |
| Tag for Docker Hub | `docker tag sparta-node:v1 mrmri9/sparta-node:v1` | Prepares the image for upload. |
| Push to Docker Hub | `docker push mrmri9/sparta-node:v1` | Uploads the image to Docker Hub. |
| Remove local image | `docker rmi sparta-node:v1` | Deletes the local copy. |
| Pull and run from Docker Hub | `docker run -d -p 3000:3000 --name fresh-sparta-node mrmri9/sparta-node:v1` | Ensures the latest version is used. |
| Remove conflicting container | `docker rm fresh-sparta-node` | Fixes duplicate container name issue. |
| Run on a different port | `docker run -d -p 3010:3000 --name fresh-sparta-node mrmri9/sparta-node:v1` | Avoids port conflicts. |



## Task 9:


| **Topic** | **Key Points** |
|-----------|--------------|
| **Why use Docker Compose?** | Simplifies multi-container management, networking, and scaling. |
| **Installation** | Comes with Docker Desktop; install manually on Linux. |
| **File Storage** | `docker-compose.yml` in the project root. |
| **Starting Application** | `docker-compose up` (foreground), `docker-compose up -d` (background). |
| **Stopping Application** | `docker-compose down` removes containers. |
| **Checking Services** | `docker-compose ps` lists running services. |
| **Viewing Logs** | `docker-compose logs -f` for real-time logs. |
| **Managing Images** | `docker-compose images` shows project images. |

---


## Task 10:

# ** Summary of Fixes & Next Steps**
| Issue | Fix |
|-----------------|--------------------------------|
| `Cannot GET /posts` | Set `DB_HOST` in `docker-compose.yml` and restarted. |
| MongoDB not connecting | Set `DB_HOST` manually, updated `docker-compose.yml`. |
| TTY error in Git Bash | Used `winpty` before `docker exec`. |
| Missing `index.ejs` | Verified file existence and added missing template. |


