# craft-docker

Docker setup for Craft cms (or any web project with similar requirements).

Files will be served from your project's `web` directory.

[docker-compose](https://docs.docker.com/compose/) is used to orchestrate 3 containers based on `nginx`, `php-fpm 7.x`, and `PostgreSQL 9.6`.

## Installation

Copy the files provided in this repository into your Craft cms project.

## Configuration

The ports exposed by the containers on localhost can be configured in `docker-compose.yaml`.

Database credentials can be configured in that file as well.

## Running the Containers

Run `docker-compose up` to start the containers.

Run `docker-compose down` to stop them.

By default, `nginx` can be reached at `http://localhost:8080`.

By default, `PostgreSQL` exposes port `5433` on localhost.

See section `Configuration` above on how to change these ports.

## Scripts

The following scripts are provided to facilitate managing the `php-fpm` container:

- `bin/bash`: opens a shell within the `php-fpm` container

- `bin/composer-install`: runs `composer install` within the `php-fpm` container and in the project directory (where `composer.json` is usually located).