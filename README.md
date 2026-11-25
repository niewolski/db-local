# postgres-local

Szablon lokalnej bazy danych w Dockerze: **PostgreSQL** albo **MySQL** (albo obie naraz).

## Jak użyć

1. Skopiuj plik ze zmiennymi:
   ```bash
   cp .env.example .env
   ```
2. W `.env` uzupełnij sekcję bazy, której używasz (`POSTGRES_*` albo `MYSQL_*`).
3. W `docker-compose.yml` odkomentuj blok tej bazy **oraz** jej wolumen w sekcji `volumes:` na dole.
4. Uruchom:
   ```bash
   docker compose up -d
   ```

## Dane połączenia

| | PostgreSQL | MySQL |
|---|---|---|
| Host | `localhost` | `localhost` |
| Port | `POSTGRES_PORT` (domyślnie 5432) | `MYSQL_PORT` (domyślnie 3306) |
| Użytkownik | `POSTGRES_USER` | `MYSQL_USER` (lub `root`) |
| Hasło | `POSTGRES_PASSWORD` | `MYSQL_PASSWORD` (root: `MYSQL_ROOT_PASSWORD`) |
| Baza | `POSTGRES_DB` | `MYSQL_DATABASE` |
| URL | `postgresql://user:pass@localhost:5432/db` | `mysql://user:pass@localhost:3306/db` |
