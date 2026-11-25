# postgres-local

Szablon lokalnych baz danych w Dockerze. Każda baza to osobny, zakomentowany blok w `docker-compose.yml`: odkomentowujesz te, których potrzebujesz (jedną albo kilka naraz).

## Jak użyć

1. Skopiuj plik ze zmiennymi:
   ```bash
   cp .env.example .env
   ```
2. W `.env` uzupełnij sekcję bazy, której używasz.
3. W `docker-compose.yml` odkomentuj blok tej bazy **oraz** jej wolumen w sekcji `volumes:` na dole.
4. Uruchom:
   ```bash
   docker compose up -d
   ```

## Bazy

Host zawsze `localhost`, port to zmienna `*_PORT` z `.env` (w nawiasie wartość domyślna).

### PostgreSQL
- Port: `POSTGRES_PORT` (5432)
- Użytkownik / hasło: `POSTGRES_USER` / `POSTGRES_PASSWORD`
- Baza: `POSTGRES_DB`
- URL: `postgresql://user:pass@localhost:5432/db`

### MySQL
- Port: `MYSQL_PORT` (3306)
- Użytkownik / hasło: `MYSQL_USER` / `MYSQL_PASSWORD` (root: `MYSQL_ROOT_PASSWORD`)
- Baza: `MYSQL_DATABASE`
- URL: `mysql://user:pass@localhost:3306/db`

### MariaDB
- Port: `MARIADB_PORT` (3307, żeby działała obok MySQL)
- Użytkownik / hasło: `MARIADB_USER` / `MARIADB_PASSWORD` (root: `MARIADB_ROOT_PASSWORD`)
- Baza: `MARIADB_DATABASE`
- URL: `mysql://user:pass@localhost:3307/db` (MariaDB jest kompatybilna z klientami MySQL)
