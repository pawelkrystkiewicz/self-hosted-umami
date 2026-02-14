# Self-Hosted Umami

[Umami](https://umami.is/) analytics deployed via Docker Compose on [Dokploy](https://dokploy.com/).

## Prerequisites

- Dokploy instance with Docker Compose support
- PostgreSQL database (can be provisioned in Dokploy)

## Setup

### 1. Create a PostgreSQL database

In Dokploy, create a PostgreSQL database and note the connection string.

### 2. Configure environment variables

Copy the example and fill in your values:

```bash
cp .env.example .env
```

| Variable | Description |
|---|---|
| `DATABASE_URL` | PostgreSQL connection string, e.g. `postgresql://user:password@host:5432/umami` |
| `APP_SECRET` | Random secret for hashing. Generate with: `openssl rand -hex 32` |

### 3. Deploy in Dokploy

1. Create a new **Compose** project in Dokploy
2. Point it to this repository (or paste the `docker-compose.yml` contents)
3. Set the environment variables from step 2

> **Networking:** Docker Compose projects in Dokploy run in an isolated network by default, which means they can't reach databases and other services managed by Dokploy. That's why `docker-compose.yml` explicitly joins `dokploy-network` — the shared network where Dokploy places its managed databases and applications.

### 4. Add a domain

In the Dokploy project settings, add your domain and set the port to **3000** (the port Umami listens on inside the container). Dokploy's Traefik reverse proxy will handle routing automatically.

### 5. First login

Default credentials:

- **Username:** `admin`
- **Password:** `umami`

**Change these immediately after first login.**
