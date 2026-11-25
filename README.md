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

### SQL Server
- Port: `MSSQL_PORT` (1433)
- Użytkownik / hasło: `sa` / `MSSQL_SA_PASSWORD` (min. 8 znaków, wielkie i małe litery, cyfry lub znaki specjalne; za słabe hasło = kontener się nie uruchomi)
- Baza: obraz nie tworzy bazy sam, utwórz ją po starcie (`CREATE DATABASE nazwa;`)
- Connection string: `Server=localhost,1433;User Id=sa;Password=...;TrustServerCertificate=True`
- Edycja Developer (darmowa do developmentu). Obraz jest tylko na amd64, na Macu z M-chipem działa przez emulację, więc wolniej.

### Redis
- Port: `REDIS_PORT` (6379)
- Hasło: `REDIS_PASSWORD` (bez użytkownika, logujesz się jako `default`)
- Dane zapisywane na dysk (AOF), więc przetrwają restart kontenera
- URL: `redis://:pass@localhost:6379/0`

### MongoDB
- Port: `MONGO_PORT` (27017)
- Użytkownik / hasło: `MONGO_USER` / `MONGO_PASSWORD` (to konto root, zapisane w bazie `admin`)
- Baza: `MONGO_DATABASE` (domyślna baza dla skryptów startowych, sama baza pojawi się przy pierwszym zapisie)
- URL: `mongodb://user:pass@localhost:27017/db?authSource=admin`

## Panele do przeglądania baz

### Adminer
Jeden lekki panel w przeglądarce dla PostgreSQL, MySQL i MariaDB.
- Adres: http://localhost:8080 (`ADMINER_PORT`)
- Logowanie: wybierz system, jako **Serwer** wpisz nazwę usługi z compose (`postgres`, `mysql`, `mariadb`), a nie `localhost`, bo Adminer działa w swoim kontenerze
- Do SQL Server i MongoDB użyj innego narzędzia (np. DBeaver, MongoDB Compass)
