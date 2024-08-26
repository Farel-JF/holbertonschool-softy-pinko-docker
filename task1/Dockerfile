# Use the latest Ubuntu image as the base
FROM ubuntu:latest

# Update and upgrade the system packages
RUN apt-get update && apt-get upgrade -y

# Install Python3 and pip3
RUN apt-get install -y python3 python3-pip

# If you get a "This environment is externally managed" error, remove the EXTERNALLY-MANAGED file
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED

# Install Flask using pip3
RUN pip3 install flask

# Set the working directory to /app
WORKDIR /app

# Copy the Python file to the Docker image
COPY ./api.py /app/api.py

# Command to run the Flask server
CMD ["python3", "/app/api.py"]
