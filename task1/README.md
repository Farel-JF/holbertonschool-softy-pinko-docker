# Task 1: Docker Flask Server

## Overview

This task demonstrates how to set up a Docker container that runs a Python Flask application. The application provides a simple "Hello, World!" response on the `/api/hello` endpoint.

## Dockerfile Explanation

The Dockerfile installs Python3, pip3, and Flask on an Ubuntu base image. It also includes a command to remove the `EXTERNALLY-MANAGED` file to avoid errors when installing packages with pip3.

## Steps to Build and Run

1. **Build the Docker Image**:
   ```bash
   docker build -t softy-pinko:task1 .
