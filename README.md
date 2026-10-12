# Docker Assignment 3: Run a Node.js Application Using Alpine Linux

## Project Overview

This project demonstrates how to create a Docker image using Alpine Linux and run a simple Node.js application inside a Docker container.

The application uses Node.js's built-in `os` module to retrieve the container's hostname and print a greeting message.

The main objective of this assignment is to understand Dockerfile instructions, install Node.js in an Alpine Linux image, build a custom Docker image, and run a container.

## Objectives

- Create a Node.js application using `index.js`.
- Use Alpine Linux as the base image.
- Add author/maintainer information to the Dockerfile.
- Update Alpine packages and install Node.js.
- Copy application files into the container.
- Set the working directory to `/app`.
- Configure the default container command.
- Build a Docker image with the name `hello:v0.1`.
- Run the container and verify the application output.

## Technologies Used

- **Docker:** For building images and running containers.
- **Alpine Linux:** A lightweight Linux distribution used as the base image.
- **Node.js:** JavaScript runtime used to execute the application.
- **JavaScript:** Programming language used to write the application.
- **Ubuntu EC2:** Environment used to perform the assignment.

## Project Structure

```text
docker-assignment-03/
├── Dockerfile
├── index.js
└── README.md
```

## Step 1: Create the Project Directory

Create a directory for the assignment and navigate into it.

```bash
mkdir docker-assignment-03
cd docker-assignment-03
```

## Step 2: Create the Node.js Application

Create a file named `index.js`.

```bash
nano index.js
```

Add the following code:

```javascript
var os = require("os");
var hostname = os.hostname();
console.log("hello from " + hostname);
```

### Explanation

- `require("os")` imports Node.js's built-in operating system module.
- `os.hostname()` retrieves the hostname of the environment where the application runs.
- `console.log()` prints the greeting message and hostname.

Example output:

```text
hello from 280a5e0e5dd8
```

The hostname may change when a new container is created.

## Step 3: Create the Dockerfile

Create a file named `Dockerfile`.

```bash
nano Dockerfile
```

Add the following instructions:

```dockerfile
FROM alpine:latest

MAINTAINER Jeetendra Singh

RUN apk update && apk add --no-cache nodejs

COPY . /app

WORKDIR /app

CMD ["node", "index.js"]
```

### Dockerfile Instructions Explained

**1. FROM alpine:latest**

Uses the latest Alpine Linux image as the base image.

**2. MAINTAINER Jeetendra Singh**

Adds the assignment author's name. This instruction is deprecated in modern Docker versions, but it is included here to meet the assignment requirements.

**3. RUN apk update && apk add --no-cache nodejs**

Updates the Alpine package index and installs Node.js. The `--no-cache` option avoids retaining the package index as a local package-manager cache.

**4. COPY . /app**

Copies the files from the build context into the `/app` directory inside the image.

**5. WORKDIR /app**

Sets `/app` as the working directory for subsequent instructions and the default command.

**6. CMD ["node", "index.js"]**

Configures the default command to execute `index.js` when a container starts.

## Step 4: Build the Docker Image

Run the following command from the directory containing the Dockerfile:

```bash
docker build -t hello:v0.1 .
```

### Command Explanation

- `docker build` builds a Docker image.
- `-t` assigns a name and tag to the image.
- `hello` is the image name.
- `v0.1` is the image tag.
- `.` specifies the current directory as the build context.

### Expected Result

```text
Successfully built 31ca8346b069
Successfully tagged hello:v0.1
```

The image ID may differ on another build.

## Step 5: Verify the Docker Image

Run:

```bash
docker images
```

Confirm that the image named `hello` has the tag `v0.1`.

Example:

```text
REPOSITORY   TAG
hello        v0.1
```

## Step 6: Run the Docker Container

Execute the application using the newly created image:

```bash
docker run --rm hello:v0.1
```

### Command Explanation

- `docker run` creates and starts a container.
- `--rm` automatically removes the container after it exits.
- `hello:v0.1` specifies the image to use.

### Actual Output

```text
hello from 280a5e0e5dd8
```

The application successfully printed the hostname of the running container.

## Step 7: Verify the Project Files

Run:

```bash
ls -l
```

Verify that the directory contains:

- `Dockerfile`
- `index.js`
- `README.md`

## Key Learnings

Through this assignment, I learned:

1. How to create and run a simple Node.js application.
2. How to use Alpine Linux as a lightweight Docker base image.
3. How to install packages using the Alpine package manager (`apk`).
4. How to write and understand Dockerfile instructions.
5. How to build and tag a custom Docker image.
6. How to run a container and verify its output.
7. How to use `docker images` to inspect locally available images.
8. How to use the `--rm` option to automatically clean up an exited container.

## Conclusion

This assignment was completed successfully. I created a Node.js application, packaged it into a custom Docker image using Alpine Linux, and ran it inside a Docker container.

The image was tagged as `hello:v0.1`, and the application printed the container hostname as expected.

**Author:** Jeetendra Singh

**Assignment:** Docker Assignment 3
