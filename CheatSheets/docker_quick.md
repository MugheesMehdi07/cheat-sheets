
```markdown
# Docker Cheat Sheet

## Basic Docker Concepts

- **Image**: A blueprint for creating Docker containers.
- **Container**: An instance of an image, running as a process.
- **Dockerfile**: A script containing a series of instructions to build a Docker image.
- **Volume**: Persistent data storage that can be attached to containers.
- **Docker Compose**: A tool for defining and running multi-container Docker applications.

## Installation

- Install Docker from the official Docker website or use package managers like `apt` for Linux, `brew` for macOS, etc.

## Docker Command Basics

### Images

- **List images**: 
  ```bash
  docker images
  ```
- **Pull an image**:
  ```bash
  docker pull [image_name]
  ```
- **Build an image**:
  ```bash
  docker build -t [image_name] .
  ```
- **Remove an image**:
  ```bash
  docker rmi [image_name]
  ```

### Containers

- **List running containers**:
  ```bash
  docker ps
  ```
- **List all containers**:
  ```bash
  docker ps -a
  ```
- **Run a container**:
  ```bash
  docker run [options] [image_name]
  ```
- **Stop a container**:
  ```bash
  docker stop [container_id]
  ```
- **Start a stopped container**:
  ```bash
  docker start [container_id]
  ```
- **Remove a container**:
  ```bash
  docker rm [container_id]
  ```

## Docker Run Options

- **Run in detached mode**:
  ```bash
  docker run -d [image_name]
  ```
- **Port mapping**:
  ```bash
  docker run -p [host_port]:[container_port] [image_name]
  ```
- **Mount volume**:
  ```bash
  docker run -v [host_dir]:[container_dir] [image_name]
  ```
- **Environment variables**:
  ```bash
  docker run -e [VAR]=[value] [image_name]
  ```
- **Run interactively**:
  ```bash
  docker run -it [image_name] [command]
  ```

## Dockerfile Instructions

- **FROM**: Base image to use.
- **RUN**: Run commands in a new layer on top of the current image.
- **COPY**: Copy files from the host to the image.
- **ADD**: Similar to COPY but can handle remote URLs and tar extraction.
- **CMD**: Default command to run when starting a container.
- **ENTRYPOINT**: Define the executable invoked when the container is started.
- **ENV**: Set environment variables.
- **EXPOSE**: Expose a port.
- **VOLUME**: Define a volume to be used by containers.
- **WORKDIR**: Set the working directory.

## Docker Compose

- **Compose file**: A `docker-compose.yml` file defines services, networks, and volumes.
- **Start services**:
  ```bash
  docker-compose up
  ```
- **Stop services**:
  ```bash
  docker-compose down
  ```

## Volume Management

- **Create a volume**:
  ```bash
  docker volume create [volume_name]
  ```
- **List volumes**:
  ```bash
  docker volume ls
  ```
- **Remove a volume**:
  ```bash
  docker volume rm [volume_name]
  ```

## Network Management

- **Create a network**:
  ```bash
  docker network create [network_name]
  ```
- **List networks**:
  ```bash
  docker network ls
  ```
- **Remove a network**:
  ```bash
  docker network rm [network_name]
  ```

## Dockerfile Example

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the current directory contents into the container at /usr/src/app
COPY . .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

## Docker Compose Example

```yaml
version: '3'

services:
  web:
    build: .
    ports:
     - "5000:5000"
  redis:
    image: "redis:alpine"
```


### Dockerfile for Django App

Create a `Dockerfile` in your Django project directory:

```Dockerfile
# Use an official Python runtime as a base image
FROM python:3.8

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR /app

# Install system dependencies
RUN apt-get update \
  && apt-get -y install libpq-dev gcc \
  && apt-get clean

# Install Python dependencies
COPY requirements.txt /app/
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# Copy the current directory contents into the container at /app/
COPY . /app/

# Collect static files
RUN python manage.py collectstatic --no-input

# Expose the port the app runs on
EXPOSE 8000

# Command to run the application
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "myproject.wsgi:application"]
```

Replace `myproject.wsgi:application` with your Django project's WSGI application path.

### docker-compose.yml for Django and PostgreSQL

Create a `docker-compose.yml` file in your project's root directory:

```yaml
version: '3.8'

services:
  db:
    image: postgres:12
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=mydatabase
      - POSTGRES_USER=myuser
      - POSTGRES_PASSWORD=mypassword

  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    environment:
      - SECRET_KEY=your_secret_key
      - DEBUG=1
      - DB_NAME=mydatabase
      - DB_USER=myuser
      - DB_PASSWORD=mypassword
      - DB_HOST=db
      - DB_PORT=5432
    depends_on:
      - db

volumes:
  postgres_data:
```

In this setup:

- The `db` service uses the official PostgreSQL image.
- The `web` service builds from the Dockerfile in your project, connects to PostgreSQL, and runs the Django app.
- Environment variables are set for both the Django app and PostgreSQL.
- A named volume `postgres_data` is used to persist database data.

### Notes:

1. Adjust environment variables (`POSTGRES_DB`, `POSTGRES_USER`, `POSTGRES_PASSWORD`, `SECRET_KEY`, etc.) as per your requirements.
2. For production deployments, remove `DEBUG=1`, configure a more secure setup, and consider using a `.env` file for environment variables.
3. This setup assumes your Django app's settings are configured to use these environment variables for database settings and other configurations.

With these configurations, your Django app will run as a microservice alongside a PostgreSQL database service, both orchestrated by Docker Compose.
