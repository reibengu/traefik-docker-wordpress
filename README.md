# Traefik Docker Configuration for WordPress, MySQL, and Adminer

This example project demonstrates how to configure [Traefik](https://traefik.io) with Docker to run a WordPress website, MySQL database, and Adminer for database management. It also includes the setup of local SSL certificates using the [mkcert](https://github.com/FiloSottile/mkcert) library for secure communication.

## Prerequisites

Before getting started with this project, make sure you have the following tools and software installed:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- [mkcert](https://github.com/FiloSottile/mkcert)

## Getting Started

1. Clone this repository to your local machine.

```bash
git clone https://github.com/reibengu/traefik-docker-wordpress.git
cd traefik-docker-wordpress
```

2. Generate local SSL certificates using mkcert. This step will provide you with SSL certificates for your local development environment.

```bash
mkcert -install
mkcert -cert-file ./certs/local-cert.pem -key-file ./certs/local-key.pem traefik.test "*.traefik.test"
```

3. Update the `/etc/hosts` file. To map the configured domains to your local machine's IP address, you'll need to add entries to your `/etc/hosts` file. Open a terminal and run the following command to edit the file:

```bash
sudo nano /etc/hosts
```

Add the following entries to the file, associating each domain with your local IP address:

```bash
127.0.0.1 monitor.traefik.test
127.0.0.1 traefik.test
127.0.0.1 blog.traefik.test
127.0.0.1 db-admin.traefik.test
```

3. Start the services using Docker Compose.

```bash
docker-compose up -d
```

This will launch Traefik, WordPress, MySQL, and Adminer containers. Traefik will automatically generate and manage SSL certificates for your services.

4. Access your services using the custom domains in your browser:

- Traefik Dashboard: https://monitor.traefik.test
- Whoami: https://traefik.test
- Adminer (Database management): https://db-admin.traefik.test (MYSQL_ROOT_PASSWORD: test)
- WordPress: https://blog.traefik.test

## Accessing Containers
You can access the individual containers directly for debugging or management purposes:

- WordPress Container: `docker exec -it traefik-blog-1 bash`
- MySQL Container: `docker exec -it traefik-db-1 bash`

## Security Considerations
This project is intended for local development purposes and may not be suitable for production use. Please ensure that you implement proper security measures, such as securing sensitive data and using real SSL certificates, when deploying to a production environment.

## Issues and Contributions
If you encounter any issues or have suggestions for improvements, please open an issue on the GitHub repository.

Happy coding!
