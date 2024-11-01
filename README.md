# Keycloak with MySQL and NGINX on Docker Compose

This guide explains how to set up a Keycloak instance with MySQL, proxied by NGINX, using Docker Compose on Ubuntu 22.04.

## Prerequisites

Before you begin, ensure that the following software is installed on your system:

- Git
- Docker
- Docker Compose

## Step 1: Clone the Repository

Clone the repository containing the Docker configuration files:

```bash
git clone https://github.com/Mazen2542-Ibrahim/Keycloak-with-MySQL-and-NGINX-on-Docker-Compose.git

cd Keycloak-with-MySQL-and-NGINX-on-Docker-Compose
```

## Step 2: Create a Folder for Certificates

Create a folder named `certs` in your project directory and add your SSL certificate files (e.g., `fullchain.pem` and `privkey.pem`).

```bash
mkdir certs
# Add your certificate files to the certs folder
```

## Step 3: Update NGINX Configuration

Edit the `nginx.conf` file to specify the correct certificate file names. Ensure they match those in your `certs` directory:

```bash
# Example NGINX configuration snippet
ssl_certificate /etc/nginx/certs/fullchain.pem;
ssl_certificate_key /etc/nginx/certs/privkey.pem;
```

## Step 4: Configure Environment Variables

Rename the `.env.example` file to `.env` and add your own database credentials and other necessary environment variables.

```bash
mv .env.example .env
# Edit the .env file to include your database credentials
```

## Step 5: Start the Docker Containers

Start the containers using Docker Compose:

```bash
docker-compose up -d
```

Verify that the services are running:

```bash
docker-compose ps
```

You can also check logs for each service. For example, to see Keycloak logs:

```bash
docker-compose logs -f keycloak
```

## Step 6: Access Keycloak

- URL: Access your Keycloak instance at `http://your-server-ip` or `https://your-domain`

- Admin Credentials: Use the `KEYCLOAK_ADMIN` and `KEYCLOAK_ADMIN_PASSWORD` from `.env`.

## Step 7: Manage Docker Containers

To stop the containers:

```bash
docker-compose down
```

To restart the containers:

```bash
docker-compose up -d
```

## Troubleshooting

1. Network Errors: Ensure that Docker is properly installed and the network configuration matches the Docker Compose file.

2. Database Connection Issues: Verify that the database environment variables are correctly set in the .env file and that MySQL is running.
