# Salon Appointment Scheduler

A small Bash script and SQL schema to manage salon appointments (Postgres + psql).

## What this repo contains

- `salon.sh` — Bash script that provides a simple text menu to book appointments (connects to Postgres via `psql`).
- `salon.sql` — SQL file with the database schema and seed data (services, customers, appointments).
- `example.txt` — Example run outputs showing expected interactions.

## Prerequisites

- Linux or macOS (instructions assume `bash` as your shell).
- PostgreSQL installed and running.
- `psql` client available on your PATH.

Note: The included `salon.sh` script uses the `psql` command with the role `freecodecamp` by default:

  PSQL="psql --username=freecodecamp --dbname=salon -t -c"

You can either create a PostgreSQL role/user named `freecodecamp` (recommended for the original script), or edit `salon.sh` to use a different username.

## Quick setup

1. Clone the repo:

```
git clone https://github.com/BoruIsakoJ/Salon-Appointment-Scheduler.git
cd "Salon-Appointment-Scheduler"
```

2. Create the database and load the schema. Open a terminal with a PostgreSQL superuser (for example `postgres`) and run:

```
# create the database
createdb salon

# load tables and seed data from the provided SQL file
psql --username=$(whoami) --dbname=salon -f salon.sql
```

If you created a `freecodecamp` role and want the script to run without edits, run the SQL as that role or make the role first. Example (run as a superuser):

```
createuser freecodecamp -s
psql -d salon -c "ALTER USER freecodecamp WITH PASSWORD 'yourpassword';"
psql --username=freecodecamp --dbname=salon -f salon.sql
```

3. Make the Bash script executable (optional) and run it:

```
chmod +x salon.sh
./salon.sh
```

Or run with bash explicitly:

```
bash salon.sh
```

## Example interaction

See `example.txt` for two sample runs showing expected prompts and outputs. The script will list services, prompt for a service number, ask for phone number and (if needed) name, then ask for an appointment time and insert an appointment.

## Troubleshooting

- psql: command not found — install the PostgreSQL client (package usually called `postgresql` or `postgresql-client`).
- Permission denied when creating DB — run `createdb` as a PostgreSQL superuser or use `sudo -u postgres createdb salon`.
- Script still failing to connect — either create the `freecodecamp` role, or edit the `PSQL` variable at the top of `salon.sh` to use an existing user: e.g.

  PSQL="psql --username=youruser --dbname=salon -t -c"

- SQL file path issues — make sure you run `psql -f salon.sql` from the repo root or provide the correct path to `salon.sql`.

## Notes and suggestions

- The script is intentionally simple for learning purposes. If you want to run it on another OS or in CI, ensure PostgreSQL is available and update the connection settings.
- Small improvements you might add: validation of numeric service IDs, trimming whitespace from inputs, better time format checks, or prettier output.

If you want, I can also add a small `Makefile` or scripts to automate DB creation and seeding.

---

Happy booking!