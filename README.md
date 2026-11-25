# postgres-local

Docker Compose template for local databases. Every service in `docker-compose.yml` is commented out, so you uncomment only the ones you need.

## Usage

1. Copy the env file and fill in the section for your database:
   ```bash
   cp .env.example .env
   ```
2. In `docker-compose.yml`, uncomment the service **and** its volume at the bottom.
3. Start it:
   ```bash
   docker compose up -d
   ```

## Services

| Service | Port | Login |
|---|---|---|
| PostgreSQL | 5432 | `POSTGRES_USER` / `POSTGRES_PASSWORD` |
| MySQL | 3306 | `MYSQL_USER` / `MYSQL_PASSWORD` |
| MariaDB | 3307 | `MARIADB_USER` / `MARIADB_PASSWORD` |
| SQL Server | 1433 | `sa` / `MSSQL_SA_PASSWORD` |
| Redis | 6379 | `REDIS_PASSWORD` |
| MongoDB | 27017 | `MONGO_USER` / `MONGO_PASSWORD` |
| Adminer | [8080](http://localhost:8080) | any SQL database above |
| pgAdmin | [5050](http://localhost:5050) | `PGADMIN_EMAIL` / `PGADMIN_PASSWORD` |

Ports can be changed with the `*_PORT` variables in `.env`.

## Notes

- **SQL Server:** the password needs at least 8 characters with uppercase, lowercase and digits or symbols, otherwise the container won't start. There is no arm64 image, so it runs under emulation on Apple Silicon.
- **MongoDB:** the user is created in the `admin` database, so connect with `?authSource=admin`.
- **pgAdmin:** `PGADMIN_EMAIL` must be a valid email address, e.g. `admin@example.com`.
- **Adminer / pgAdmin:** to connect to a database, use the service name as the host (`postgres`, `mysql`, `mariadb`), not `localhost`.
