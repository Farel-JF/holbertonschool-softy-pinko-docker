# holbertonschool-softy-pinko-docker

Docker Project: Reverse Proxy, Load Balancer, and Multiple Servers Setup
Overview
This project demonstrates how to set up an application infrastructure using Docker that includes:

A Reverse Proxy server that serves as the entry point for your application.
A Load Balancer that distributes traffic across two API servers using the Round Robin algorithm.
Two API Servers that handle backend logic and processing.
One Front-End Server that serves static content to the client.
With this setup, you will learn how to use Docker and Docker Compose to manage multiple containers and services efficiently.

Prerequisites
Before starting, ensure that you have the following installed on your local computer:

Docker Desktop - Download and install Docker Desktop for your operating system:

Docker Desktop for Windows
Docker Desktop for Mac
Docker Desktop for Linux
Note: Chromebook users can install the Docker engine but not Docker Desktop. It is recommended to use a Windows, Mac, or Linux machine.
Basic Knowledge of Docker - Familiarize yourself with Docker basics using the Docker Tutorial.

Architecture Overview
The infrastructure for this project consists of the following components:

Reverse Proxy and Load Balancer:

Acts as the entry point for all incoming requests.
Routes requests to either the API servers or the front-end server.
Balances traffic between the two API servers using a Round Robin load-balancing algorithm.
API Servers (2 Instances):

Handle the backend processing.
Serve requests routed by the load balancer.
Front-End Server:

Serves static content to the client.
The content is routed through the reverse proxy.
High-Level Design
When traffic enters the system:

For Front-End Content: Requests for static content are routed to the front-end server. The reverse proxy handles communication with the client, so the client never directly accesses the front-end server.

For API Requests: Requests are first routed to the load balancer, which uses the Round Robin algorithm to distribute requests evenly between the two API servers. The reverse proxy manages the communication, so the client does not directly interact with the API servers.

Step-by-Step Setup Guide
1. Clone the Repository
Clone the project repository from GitHub (replace <repository-url> with your repository's URL):

bash
Copy code
git clone <repository-url>
cd <repository-folder>
2. Set Up Docker Containers
We will use Docker Compose to manage our multi-container application.

Create a docker-compose.yml File
Create a docker-compose.yml file in your project directory with the following content:

yaml
Copy code
version: '3.8'

services:
  reverse-proxy:
    image: nginx:latest
    container_name: reverse-proxy
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - api-server-1
      - api-server-2
      - front-end

  api-server-1:
    image: your-api-image
    container_name: api-server-1
    environment:
      - NODE_ENV=production

  api-server-2:
    image: your-api-image
    container_name: api-server-2
    environment:
      - NODE_ENV=production

  front-end:
    image: your-frontend-image
    container_name: front-end
    environment:
      - NODE_ENV=production
Make sure to replace your-api-image and your-frontend-image with the actual Docker images for your API and front-end servers.

Create an NGINX Configuration File
Create an nginx.conf file in the same directory to configure the reverse proxy and load balancer:

nginx
Copy code
events {}

http {
    upstream api_servers {
        server api-server-1:80;
        server api-server-2:80;
    }

    server {
        listen 80;

        location /api/ {
            proxy_pass http://api_servers;
        }

        location / {
            proxy_pass http://front-end;
        }
    }
}
3. Build and Run the Containers
With Docker Compose set up, you can now build and start your containers:

bash
Copy code
docker-compose up --build
This command will build the Docker images if needed and start all containers as defined in the docker-compose.yml file.

4. Access Your Application
API Requests: Navigate to http://localhost/api/ to access the API endpoints.
Front-End Content: Navigate to http://localhost/ to access the front-end static content.
5. Stopping and Removing Containers
To stop and remove all running containers, use:

bash
Copy code
docker-compose down
Additional Notes
Round Robin Load Balancing: This project uses a Round Robin algorithm for load balancing, which distributes requests sequentially across the two API servers.
Scaling: You can easily scale the number of API servers by updating the docker-compose.yml file and adding more instances under the api_servers upstream block in the nginx.conf file.
Customization: Feel free to modify the Docker images, environment variables, and configuration files to suit your needs.
Conclusion
This project demonstrates the basics of setting up a scalable, Docker-based infrastructure with a reverse proxy, load balancer, multiple application servers, and a front-end server. By following these steps, you can deploy similar setups for your own applications and leverage Docker's portability and scalability features.
