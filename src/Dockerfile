# Use the Ubuntu base image
FROM ubuntu:latest

# Create a non-root user with a home directory
RUN useradd -m ansible

# Install system dependencies as root
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv sshpass && \
    rm -rf /var/lib/apt/lists/*

# Set up virtual environment and install Ansible as the non-root user
USER ansible

# Set the working directory to the non-root user's home directory
WORKDIR /home/ansible

# Set up Python virtual environment and install Ansible
RUN python3 -m venv ansible-env && \
    ./ansible-env/bin/pip install --upgrade pip && \
    ./ansible-env/bin/pip install ansible

# Update PATH to include the virtual environment's bin directory
ENV PATH="/home/ansible/ansible-env/bin:$PATH"

# Create a directory for the workspace
RUN mkdir /home/ansible/workspace

# Set the working directory to the workspace
WORKDIR /home/ansible/workspace
