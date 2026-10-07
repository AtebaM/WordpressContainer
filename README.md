# WordPress Dockerized Project

---

## Description

This repository provides a ready-to-use DevOps architecture, containerized via **Docker** and **Docker Compose**, to run a **WordPress** website coupled with a **MySQL** database.

**Objectives and Features:**
* **Isolation and Portability:** Deploy a complete and functional WordPress environment in seconds, without having to install PHP, Apache, or MySQL directly on your host machine.
* **Security:** Strict separation of configurations and passwords through the use of an external environment file (`.env`).
* **Persistence:** Use of named Docker volumes (`wordpress_data` and `mysql_data`) to ensure no data (media files, themes, SQL tables) is lost when containers are stopped or removed.
* **Internal Networking:** Containers communicate securely via a dedicated Docker network (`wp_network`).

---

## Table of Contents (ToC)
1. [Description](#description)
2. [Quickstart](#quickstart)
   - [Prerequisites](#prerequisites)
   - [Quick Start Guide](#quick-start-guide)
3. [Usage and Configuration](#usage-and-configuration)
   - [Project Structure](#project-structure)
   - [Environment Variables (`.env`)](#environment-variables-env)
   - [Customizing Ports and Services](#customizing-ports-and-services)
   - [Data Persistence (Volumes)](#data-persistence-volumes)



## Quickstart

### Prerequisites
Before you begin, make sure you have the following installed on your machine:
* [Docker](https://docs.docker.com/get-docker/)
* [Docker Compose](https://docs.docker.com/compose/install/)

### Quick Start Guide

### Prerequisites
Before running the server, ensure you have the following installed on your host system:
* [Docker Engine](https://docs.docker.com/get-docker/) (v20.10.0 or higher)
* [Docker Compose](https://docs.docker.com/compose/install/) (v2.0.0 or higher)

### Starting the Server

1. **Clone or place the project files** into a folder on your machine.
2. **Create a `.env` file** at the root of the project based on the default configuration (see the [Usage](#usage-and-configuration) section).
3. **Start the containers** in the background using the following command:
   ```bash
   docker compose up -d
   ```


## Usage and Configuration

 This section details the file structure and how to modify settings to tailor the project to your needs.

## Repository Content
Every file included in this repository serves a specific purpose

* **`.gitignore`**: Defines patterns to exclude local data directories, environment files, and temporary logs from Git tracking.
* **`docker-compose.yaml`**: Orchestrates the `wordpress-server` service, managing port forwarding, environment variables, restart policies, and persistent storage volumes.
* **`README.md`**: Project documentation providing setup instructions, technical details, and usage guides.
* **`.env.example`**: Template listing all required environment variables without exposing sensitive values or IP addresses.
* **`Wordpress Checkliste.md`**: Formal compliance document verifying all project evaluation requirements.


## Project Structure

```
 docker-compose.yml   # Services orchestration file
.env                 # Confidential file containing environment variables

```

## Environment Variables (.env)

> [!NOTE]
>The .env file centralizes all passwords and configurable parameters. Create a file named .env(see the structure of .env.example)

How to modify it for different results?

To change the database password, simply update DB_PASSWORD and DB_ROOT_PASSWORD.

Note: If the database has already been initialized once, modifying the .env file later will not change the credentials inside the existing MySQL database (unless you remove the data volume).


## Customizing Ports and Services

In the docker-compose.yml file, the port exposed on your host machine is dynamically linked to the WORDPRESS_PORT variable.

*Changing the access port:*
If port 8080 is already in use on your machine, modify the value in your .env file:

`*WORDPRESS_PORT=8081*`

Then restart the services to apply the change:

```bash

docker compose down
docker compose up -d

```

## Data Persistence (Volumes)

WordPress and MySQL data are stored in volumes managed by Docker:

- wordpress_data : Stores source code, themes, plugins, and uploaded media (/var/www/html).

- mysql_data : Stores database files (/var/lib/mysql).

Complete Cleanup (Warning - Deletes all data):

If you want to completely reset the project and erase the database, use:

```bash
docker compose down -v
```
