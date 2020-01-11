# WordPress website (Apache/PHP and MySQL) with Docker

A WordPress based website and local Docker-based development environment. 

Source: https://akrabat.com/developing-wordpress-sites-with-docker/

## Directory/file structure:

* `app/` – The WordPress application files are in this directory.
* `bin/` – Useful command-line scripts
* `data/` – MySQL dump files go here.
* `docker/` – Files required by the Docker setup are in this directory.
* `README.md` – Every project needs a README!
* `docker-compose.yml` – Development orchestration config file.

## File `/app/wp-config.php`

```php
// ...
/** The name of the database for WordPress */
define('DB_NAME', $_SERVER['DB_NAME'] ?? $_ENV['DB_NAME'] ?? null);
 
/** MySQL database username */
define('DB_USER', $_SERVER['DB_USER'] ?? $_ENV['DB_USER'] ?? null);
 
/** MySQL database password */
define('DB_PASSWORD', $_SERVER['DB_PASSWORD'] ?? $_ENV['DB_PASSWORD'] ?? null);
 
/** MySQL hostname */
define('DB_HOST', $_SERVER['DB_HOST'] ?? $_ENV['DB_HOST'] ?? null);
// ...
```

```php
// ...
define('WP_DEBUG', (bool) ($ENV['WP_DEBUG'] ?? false));
define('WP_DEBUG_LOG', (bool) ($ENV['WP_DEBUG'] ?? false));
// ...
```

## Hostname

Set up a host name pointing at `127.0.0.1` in your `/etc/hosts`, for example, `dev.project1.com`.

```
127.0.0.1 dev.project1.com
```

## Start up

Start up with:

```bash
docker-compose up
```

Go to http://dev.project1.com and start work. Press `CTRL` + `C` to stop.

To rebuild the containers:

```bash
docker-compose up --force-recreate --build
```

To delete the `db_data` volume:

```bash
docker-compose down -v
```

## Exporting the database

To export the database into a MySQL dump file from the db container:

```bash
bin/export-db
```

## Restoring a database dump

```bash
bin/restore-db live-dump.sql
```

## Keep in mind

On Mac the magic `host.docker.internal` domain name is available, so that XDebug works. However this hostname isn’t available on Linux at least yet, so you’ll have to find a workaround if you’re on Linux.
