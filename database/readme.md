setting up a PostgreSQL database and a PgAdmin container using Dockercompose:

## Setting Up a PostgreSQL Database with Docker

To create a PostgreSQL database using Docker, follow these steps:

### Step 1: Create the PostgreSQL Container

Use the following `docker run` command to set up a PostgreSQL container with specific configurations:

```bash
docker run -itd --name postgresdb \
-e POSTGRES_USER=henry \
-e POSTGRES_PASSWORD=password \
-e PGDATA=/var/lib/postgresql/data/pgdata \
-v /custom/mount:/var/lib/postgresql/data \
-p 8897:5432 --network postgresnet postgres
```

You can customize the environment variables directly in the `docker run` command for easy access.

#### Environment Variables

You can set environment variables directly within the `docker run` command like this:

```bash
-e VARIABLE_NAME=your_value
```

#### Using `env_file` for Secrets

For sensitive data such as passwords or secret keys, it's recommended to use an `env_file` to store these values securely. Make sure to add these secrets to a file named `secrets.env`.

### Step 2: Create the `.dockerignore` File

It's a good practice to create a `.dockerignore` file to exclude unnecessary files and directories from being included in your Docker image. This file helps reduce the image size and avoid unintended inclusions.

### Step 3: Setting Up PgAdmin

To manage your PostgreSQL database easily, you can also create a PgAdmin container:

```bash
docker run -itd --name pgadmin -e PGADMIN_DEFAULT_EMAIL=henry@henry.com -e PGADMIN_DEFAULT_PASSWORD=admin -p 5050:80 --network postgresnet dpage/pgadmin4
```

### Step 4: Create Networks and Volumes

Make sure to create the necessary Docker networks and volumes for storage. These resources help organize and manage your containers effectively. You can define the networks and volumes in your Docker Compose files or set them up individually using `docker network create` and `docker volume create` commands.

