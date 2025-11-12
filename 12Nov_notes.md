#### Date: 12th November 2025
# Deep Dive into Docker Images

## 1. What is a Docker Image?
A Docker image is a read-only template used to create Docker containers. It 
contains the application code, libraries, dependencies, and environment 
settings needed for the application to run. Images are organized in layers.

## 2. Image Layers and Storage
Docker images are built-in layers. Each instruction in a Dockerfile creates a 
new layer.
- **Layered Architecture:** Layers are stacked on top of each other.
- **Read-Only:** Once an image is created, its layers are read-only.
- **Copy-on-Write (CoW):** When a container is started from an image, Docker 
  adds a thin read-write layer (container layer) on top. Any changes made to 
  the running container are stored in this layer.
- **Layer Reuse:** If multiple images share the same base layers, Docker stores 
  them only once on the disk, saving space.

## 3. The Dockerfile
A Dockerfile is a text document that contains all the commands a user could 
call on the command line to assemble an image.
Common Instructions:
- `FROM`: Specifies the base image (e.g., `FROM ubuntu:22.04`).
- `RUN`: Executes commands in a new layer (e.g., `RUN apt-get update`).
- `COPY` & `ADD`: Copy files from the host to the image.
- `WORKDIR`: Sets the working directory inside the container.
- `CMD` & `ENTRYPOINT`: Specify the command to run when the container starts.
- `ENV`: Set environment variables.
- `EXPOSE`: Indicate which ports the container listens on at runtime.

## 4. Working with Images
- **Build an image:** `docker build -t <image_name>:<tag> .`
- **Tag an image:** `docker tag <source_image> <target_image>:<tag>`
- **Push an image:** `docker push <image_name>:<tag>`
- **Pull an image:** `docker pull <image_name>:<tag>`
- **Search for images:** `docker search <name>`
- **View image history:** `docker history <image_name>`
- **Inspect image details:** `docker inspect <image_name>`

## 5. Image Tags and Versions
Tags are used to version images. The `latest` tag is default if no tag is 
specified.
- **Best Practice:** Avoid using `latest` in production. Use specific version 
  tags (e.g., `myapp:v1.2.3`) to ensure consistency across environments.

## 6. Base Images vs. Parent Images
- **Base Image:** An image that does not have a parent (often `scratch`).
- **Parent Image:** The image your Dockerfile is based on (e.g., using 
  `FROM node:20` means Node 20 is the parent image).

## 7. Optimizing Docker Images
- **Use Minimal Base Images:** Use Alpine Linux (`node:20-alpine`) to reduce 
  image size.
- **Minimize Layers:** Combine multiple `RUN` commands using `&&` and `\`.
- **Use .dockerignore:** Exclude unnecessary files (like `node_modules`, 
  `.git`) from the build context.
- **Multi-stage Builds:** Use one image for building/compiling and another 
  minimal image for running the app to keep the final production image small.

## 8. Conclusion
Docker images are the building blocks of containerized applications. 
Understanding how they are structured, layered, and optimized is key to 
efficiently managing containerized environments and building fast, secure, 
and reliable CI/CD pipelines.

---
*End of Notes*
