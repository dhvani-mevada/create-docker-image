# How to Create a Docker Image – Step-by-Step Practical

A Docker image is a package that contains your application code, dependencies, libraries, and configuration. We create a Docker image using a `Dockerfile`.

Let's create a simple Docker image using an HTML website and Nginx on your Linux system (RHEL).

---

## Step 1: Check Docker Installation

Check whether Docker is installed:
```bash
docker --version
```

Check the Docker service status:
```bash
sudo systemctl status docker
```

If Docker is not running, start and enable it:
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

---

## Step 2: Create a Project Directory

Create a new folder and navigate into it:
```bash
mkdir create-docker-image
cd create-docker-image
```

---

## Step 3: Create an HTML File

Create an `index.html` file:
```bash
vi index.html
```

Add the following code:
```html
<!DOCTYPE html>
<html>
<head>
    <title>My Docker Project</title>
</head>
<body>
    <h1>Welcome to Docker!</h1>
    <h2>My First Docker Image</h2>
    <p>Created using Dockerfile and Nginx.</p>
</body>
</html>
```

**Save the file:** Press `Esc`, type `:wq`, and press `Enter`.

---

## Step 4: Create a Dockerfile

Create a file named `Dockerfile` (without any file extension):
```bash
vi Dockerfile
```

Add the following code:
```dockerfile
# Use Nginx base image
FROM nginx:latest

# Copy HTML file into Nginx web directory
COPY index.html /usr/share/nginx/html/index.html

# Expose port 80
EXPOSE 80
```

Save and exit the file (`Esc` -> `:wq` -> `Enter`).

### Understanding Dockerfile Instructions

| Instruction | Meaning |
| :--- | :--- |
| `FROM` | Selects the base image |
| `COPY` | Copies application files |
| `EXPOSE` | Documents the application port |
| `RUN` | Executes commands while building |
| `CMD` | Defines the default startup command |

---

## Step 5: Build the Docker Image

Run the build command:
```bash
docker build -t my-docker-app:1.0 .
```

**Command Breakdown:**
* `docker build` – Creates a Docker image.
* `-t` – Gives a name and tag to the image.
* `my-docker-app` – Image name.
* `1.0` – Image version/tag.
* `.` – Current directory containing the `Dockerfile`.

**Expected Result:**
```text
Successfully built xxxxxxxxx
Successfully tagged my-docker-app:1.0
```

---

## Step 6: Check the Docker Image

Verify that your image was created:
```bash
docker images
```

You should see output similar to:
```text
REPOSITORY       TAG       IMAGE ID
my-docker-app    1.0       xxxxxxxxx
nginx            latest    xxxxxxxxx
```

---

## Step 7: Run a Docker Container

Create and start a container from your image:
```bash
docker run -d -p 8080:80 --name mycontainer my-docker-app:1.0
```

**Command Breakdown:**
* `-d` – Runs the container in detached mode (in the background).
* `-p 8080:80` – Maps host port `8080` to container port `80`.
* `--name` – Assigns a custom name to the container.
* `my-docker-app:1.0` – The Docker image to run.

---

## Step 8: Check Running Containers

List currently running containers:
```bash
docker ps
```

To check all containers (including stopped ones):
```bash
docker ps -a
```

---

## Step 9: Open Your Application

Open your web browser and visit:
* [http://localhost:8080](http://localhost:8080)

You should see your **Welcome to Docker!** webpage.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c7395451-25ef-4106-9e40-a24cd21f4f74" />

---

## Step 10: Push Docker Image to Docker Hub

1. Create an account on [Docker Hub](https://docker.com) if you don't already have one.
2. Log in from your terminal:
   ```bash
   docker login
   ```
3. Tag your image with your Docker Hub username:
   ```bash
   docker tag my-docker-app:1.0 YOUR_DOCKER_USERNAME/my-docker-app:1.0
   ```
4. Push the image to Docker Hub:
   ```bash
   docker push YOUR_DOCKER_USERNAME/my-docker-app:1.0
   ```

Now your image is available on Docker Hub!
