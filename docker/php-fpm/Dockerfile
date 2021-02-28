ARG TAG
ARG POSTGRESQL_CLIENT_VERSION

FROM php:${TAG}

ARG POSTGRESQL_CLIENT_VERSION

# RUN apt-get install -y wget apt-transport-https ca-certificates gnupg

RUN apt-get update
RUN apt-get install -y apt-transport-https
RUN apt-get install -y ca-certificates
RUN apt-get install -y gnupg
RUN apt-get install -y wget
RUN apt-get install -y vim
RUN apt-get install -y lsb-release

# gcloud cloud SDK keys and packages setup
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -

# postgres-client keys and packages setup
# RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt buster-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

RUN apt-get update

RUN apt-get install -y imagemagick
RUN apt-get install -y libmagickwand-dev --no-install-recommends
RUN apt-get install -y libzip-dev
RUN apt-get install -y libpq-dev
RUN apt-get install -y google-cloud-sdk
RUN apt-get install -y "postgresql-client-${POSTGRESQL_CLIENT_VERSION}"

# PHP extensions
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN yes '' | pecl install imagick && docker-php-ext-enable imagick
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install zip

# PHP composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
