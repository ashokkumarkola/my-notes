# PostgreSQL Cheat Sheet

## Install / run

```bash
sudo apt install postgresql postgresql-contrib
sudo systemctl status postgresql
sudo -u postgres psql                       # login as superuser

docker run -d --name pg -p 5432:5432 \
  -e POSTGRES_PASSWORD=secret postgres:16
```

## Connect

```bash
psql -h localhost -p 5432 -U postgres -d mydb
psql "postgresql://user:pass@localhost:5432/mydb"
```

## psql meta-commands

| Command | Action |
|---|---|
| `\l` | List databases |
| `\c mydb` | Connect to database |
| `\dt` | List tables |
| `\d users` | Describe table |
| `\dn` | List schemas |
| `\du` | List roles/users |
| `\di` | List indexes |
| `\x` | Toggle expanded output |
| `\timing` | Show query time |
| `\i file.sql` | Run SQL file |
| `\e` | Edit query in editor |
| `\?` / `\h SELECT` | Help |
| `\q` | Quit |

## Databases + users

```sql
CREATE DATABASE mydb;
CREATE USER app WITH PASSWORD 'secret';
GRANT ALL PRIVILEGES ON DATABASE mydb TO app;
ALTER DATABASE mydb OWNER TO app;
DROP DATABASE mydb;
```

```bash
createdb mydb
dropdb mydb
```

## Backup / restore

```bash
pg_dump -U postgres mydb > mydb.sql              # plain SQL
psql -U postgres -d mydb < mydb.sql              # restore plain
pg_dump -U postgres -Fc mydb > mydb.dump         # custom format
pg_restore -U postgres -d mydb mydb.dump
```

## Postgres-specific

| Feature | Example |
|---|---|
| Auto id | `id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY` |
| UUID | `id UUID DEFAULT gen_random_uuid()` |
| JSON | `data JSONB` · `data->>'name'` · `data @> '{"a":1}'` |
| Array | `tags TEXT[]` · `'x' = ANY(tags)` |
| Upsert | `INSERT ... ON CONFLICT (email) DO UPDATE SET age = EXCLUDED.age` |
| Return rows | `INSERT ... RETURNING id` |
| Case-insensitive match | `ILIKE` |
| Query plan | `EXPLAIN ANALYZE SELECT ...` |

## Inspect

```sql
SELECT version();
SELECT current_database(), current_user;
SELECT pg_size_pretty(pg_database_size('mydb'));
SELECT pid, state, query FROM pg_stat_activity;
```
