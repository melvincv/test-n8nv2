# Local Install of n8n v2

[![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-blue)](https://n8n.io/)
[![Docker](https://img.shields.io/badge/Docker-Compose-blue)](https://docs.docker.com/compose/)

This repository provides a simple setup to run [n8n](https://n8n.io/) v2 locally using Docker Compose. n8n is a powerful workflow automation tool that allows you to connect different services and automate tasks without coding.

## Features

- Local n8n instance with HTTPS via Traefik and Let's Encrypt
- Persistent data storage
- File access via local-files directory
- Secure encryption for sensitive data

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/)
- A domain name pointing to your server's IP (for SSL certificates)
- Git (for cloning the repository)
- An IDE like [VS Code](https://code.visualstudio.com/) (recommended)

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/melvincv/test-n8nv2.git
cd test-n8nv2
```

### 1.5. Create Local Files Directory

Create the `local-files` directory to avoid permission issues with Docker volume mounting:

```bash
mkdir local-files
```

### 2. Configure Environment Variables

Edit the `.env` file with your preferred editor:

- `DOMAIN_NAME`: Your top-level domain (e.g., `example.com`)
- `SUBDOMAIN`: The subdomain for n8n (e.g., `n8n`)
- `GENERIC_TIMEZONE`: Your timezone (e.g., `America/New_York`, `Europe/London`)
- `SSL_EMAIL`: Your email for Let's Encrypt SSL certificates (uncomment and set)
- `N8N_ENCRYPTION_KEY`: A secure 32-character string for encrypting data (uncomment and set)

**Important:** Generate a strong encryption key. You can use a tool like `openssl rand -hex 32` to create one.

### 3. Start the Services

```bash
# Pull the latest images
docker compose pull

# Start the services in detached mode
docker compose up -d

# Check that services are running
docker compose ps
```

### 4. Monitor Logs

```bash
# View logs for all services
docker compose logs --tail 100 -f
```

### 5. Access n8n

Open your browser and navigate to: `https://[SUBDOMAIN].[DOMAIN_NAME]`

For example: `https://localn8n.melvincv.com/`

### 6. Initial Setup

1. Create an admin account with your email and a strong password
2. Check your email for a license activation link
3. Click the link to activate your local n8n instance

## File Structure

- `compose.yml`: Docker Compose configuration
- `.env`: Environment variables (configure before running)
- `local-files/`: Directory for local file access within workflows
- `README.md`: This file

## Managing the Stack

### Stop the Services

```bash
docker compose down
```

### Restart Services

```bash
docker compose restart
```

### Update n8n

```bash
docker compose pull
docker compose up -d
```

### View Service Status

```bash
docker compose ps
```

## Troubleshooting

### Common Issues

1. **SSL Certificate Issues**: Ensure your domain points to the server's IP and ports 80/443 are open.

2. **Container Won't Start**: Check logs with `docker compose logs`. Ensure environment variables are set correctly.

3. **Cannot Access Web Interface**: Verify the URL matches your `SUBDOMAIN` and `DOMAIN_NAME`. Wait a few minutes for SSL certificates to generate.

4. **File Permissions**: If you encounter permission issues, ensure Docker has access to the necessary directories.

### Reset Everything

To completely reset (this will delete all data):

```bash
docker compose down -v
docker compose up -d
```

### Logs and Debugging

- Use `docker compose logs -f` to follow logs in real-time
- Check Traefik dashboard at `http://localhost:8080` (if enabled)
- Ensure no other services are using ports 80, 443, or 5678

## Contributing

Feel free to submit issues or pull requests to improve this setup.

## License

This repository is provided as-is for educational and personal use.

## Resources

- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community](https://community.n8n.io/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)