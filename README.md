# WordPress Dev Environment

This repository contains a Docker Compose setup for a local WordPress development environment. It includes Nginx, MySQL, and PHPMyAdmin, allowing you to easily run and develop themes or plugins.

## Getting Started

Follow these steps to set up the project on your local machine.

### Prerequisites

You need to have Docker and Docker Compose installed.

  * [Install Docker](https://docs.docker.com/get-docker/)
  * [Install Docker Compose](https://docs.docker.com/compose/install/)

### Installation

1.  **Clone the repository:**

    ```sh
    git clone [repository-url]
    cd [repository-name]
    ```

2.  **Create a `.env` file:**
    Copy the example environment file and rename it.

    ```sh
    cp .env.example .env
    ```

3.  **Update `.env` variables:**
    Open the newly created `.env` file and update the variables as needed. You can change the database name, user, and passwords.

4.  **Find your User and Group IDs:**
    To avoid file permission errors, you need to set your local user and group IDs in the `.env` file. Open your terminal and run the following commands to find your `UID` and `GID`:

    ```sh
    id -u
    id -g
    ```

    The output will be two numbers, for example, `1000` for both.

5.  **Set `LOCAL_UID` and `LOCAL_GID`:**
    Add the `LOCAL_UID` and `LOCAL_GID` variables to your `.env` file using the numbers you just found. This ensures the WordPress container runs with the same permissions as your local user, allowing you to modify files in the `wp-content` directory without issues.

    ```env
    LOCAL_UID=1000
    LOCAL_GID=1000
    ```

6.  **Run Docker Compose:**
    Start all the services defined in the `docker-compose.yml` file.

    ```sh
    docker compose up -d
    ```

    The `-d` flag runs the containers in the background.

7.  **Access WordPress:**
    Once the containers are up and running, you can access your WordPress site by navigating to `http://localhost:8080` in your web browser.

## Directory Structure

  * `./src`: This directory is mounted as the **`wp-content`** folder inside the WordPress container. You can add your themes and plugins here.
  * `./nginx`: Contains the Nginx configuration file. You can adjust this for specific server needs.

## Troubleshooting

### File Permissions

If you encounter `permission denied` errors when trying to edit theme or plugin files run the following command on the `src` directory:

```sh
sudo chown -R yourusername:yourusername /path/to/directory
```