# craft-docker

Docker setup for [Craft cms](https://craftcms.com/), or any web project with similar requirements.

Files will be served from your project's `web` directory.

[docker-compose](https://docs.docker.com/compose/) is used to orchestrate 3 containers based on `nginx`, `php-fpm`, and `PostgreSQL`.

The `php-fpm` container also includes a postgres client as well as the Google Cloud SDK to facilitate backing up to and restoring from Google Cloud Storage. See [thomasspitaler/craft-scripts](https://github.com/thomasspitaler/craft-scripts) for scripts to backup and restore the Craft cms database and assets.

## Installation

Copy the files provided in this repository into your Craft cms project.

Copy the provided `.env.example` file: `cp .env.example .env` or merge the contained variables into your existing `.env`, taking care not to overwrite your settings.

## Configuration

Change the variables in `.env` according to your environment, see also the provided `.env.example`.

```bash
DOCKER_PHP_FPM_TAG=7-fpm # specifies which tag/version of php-fpm to use, defaults to 7-fpm
DOCKER_PHP_FPM_POSTGRESQL_CLIENT_VERSION=13 # postgresql-client can be used to perform database dump and restore

DOCKER_NGINX_EXPOSE_PORT=8080 # nginx will be exposed at this port

DOCKER_POSTGRES_TAG=13 # specifies which tag/version of postgres to use, defaults to 13
DOCKER_POSTGRES_DATABASE="simplebytes" # name of the database
DOCKER_POSTGRES_USER="dev" # database user
DOCKER_POSTGRES_PASSWORD="dev" # database password
DOCKER_POSTGRES_EXPOSE_PORT=5432 # postgres will be exposed at this port
```

## Running the Containers

Run `docker-compose up` to start the containers.

Run `docker-compose down` to stop them.

By default, `nginx` can be reached at `http://localhost:8080`.

By default, `PostgreSQL` exposes port `5432` on localhost.

See section [Configuration](#configuration) above on how to change these ports.

## Scripts

The following scripts are provided to facilitate managing the `php-fpm` container:

- `bin/bash`: opens a shell within the `php-fpm` container

- `bin/composer`: runs `composer` within the `php-fpm` container and in the project directory (where `composer.json` is usually located).

    For example, `bin/composer install` will install packages.
