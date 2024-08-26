Step-by-Step Guide to Create the Docker Image
Create a Dockerfile: This file will define the steps needed to create the Docker image.

Build the Docker Image: Use Docker commands to build the image from the Dockerfile.

Run the Docker Image: Verify that the image is working correctly by running it in a container.

Create a README.md: Document the steps, commands, and purpose of the Docker image in a README.md file.

1. Dockerfile Content
Here is the content you should put in your Dockerfile:

Dockerfile
Copy code
# Use the latest Ubuntu image as the base
FROM ubuntu:latest

# Update and upgrade the system packages
RUN apt-get update && apt-get upgrade -y

# Command to run when the container starts
CMD echo "Hello, World!"
2. Build the Docker Image
Open your terminal, navigate to the task0 directory where your Dockerfile is located, and run the following command to build the Docker image:

bash
Copy code
docker build -t softy-pinko:task0 .
Explanation:

docker build: Docker command to build an image.
-t softy-pinko:task0: Tags the image with the name softy-pinko and the tag task0.
.: Specifies that Docker should use the Dockerfile in the current directory.
3. Run the Docker Container
Run the container from the image you just built to see if it works correctly:

bash
Copy code
docker run -it --rm --name softy-pinko-task0 softy-pinko:task0
Explanation:

docker run: Runs a Docker container.
-it: Runs the container in interactive mode with a terminal attached.
--rm: Automatically removes the container when it stops.
--name softy-pinko-task0: Names the running container softy-pinko-task0.
softy-pinko:task0: Specifies the image to use.
After running this command, you should see:

Copy code
Hello, World!
4. Create the README.md
Create a file named README.md in your task0 directory with the following content:

markdown
Copy code
# Docker Project: Task 0

## Overview

This task involves creating a simple Docker image based on the latest Ubuntu image. The Dockerfile updates the system's APT package list and upgrades the installed software packages. The container then runs a command that outputs "Hello, World!" to the terminal.

## Dockerfile

The Dockerfile used for this task is:

```Dockerfile
# Use the latest Ubuntu image as the base
FROM ubuntu:latest

# Update and upgrade the system packages
RUN apt-get update && apt-get upgrade -y

# Command to run when the container starts
CMD echo "Hello, World!"
Build the Docker Image
To build the Docker image, run the following command in your terminal:

bash
Copy code
docker build -t softy-pinko:task0 .
Run the Docker Container
To run the Docker container and see the "Hello, World!" output, execute:

bash
Copy code
docker run -it --rm --name softy-pinko-task0 softy-pinko:task0
Expected Output
After running the container, you should see the following output in your terminal:

Copy code
Hello, World!
Repository
The repository for this project is located at: GitHub: holbertonschool-softy-pinko-docker

sql
Copy code

### 5. Commit and Push Your Changes

Ensure you have added the `Dockerfile` and `README.md` to your Git repository. Here are the commands to add, commit, and push your changes:

```bash
git add Dockerfile README.md
git commit -m "Add Dockerfile and README for task0"
git push origin main
Replace main with your branch name if it’s different.

Conclusion
You have now created your first Docker image and documented the process in a README.md file. This guide should help you set up and run Docker containers effectively.
