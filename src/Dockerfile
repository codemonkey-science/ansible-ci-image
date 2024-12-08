# Use the Ubuntu base image
FROM ubuntu:latest

# Create a non-root user with a home directory
RUN useradd -m ansible

# Install system dependencies as root
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv sshpass sudo acl && \
    rm -rf /var/lib/apt/lists/*

# Set the HOME environment variable for the ansible user
ENV HOME=/home/ansible

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

# Switch back to root to set permissions
USER root

# Set permissions for the ansible user
RUN chown -R ansible:ansible /home/ansible && \
    chmod -R 755 /home/ansible

# Ensure the ansible user has permissions for the GitHub Actions workspace
RUN mkdir -p /__w && \
    chown -R ansible:ansible /__w && \
    chmod -R 777 /__w

# Github actions will make the workspace available at /github sometimes
RUN mkdir -p /github && \
    chown -R ansible:ansible /github && \
    chmod -R 777 /github && \
    setfacl -dR -m u:ansible:rwx /github && \
    setfacl -R -m u:ansible:rwx /github

# Switch back to the ansible user
USER ansible