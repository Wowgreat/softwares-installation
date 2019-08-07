### Official recommended way

[Official page](https://docs.sentry.io/server/installation/docker/)

- ```shell
  git clone https://github.com/getsentry/onpremise.git
  # if you want to push it to a registry
  REPOSITORY={yorprivateregistry}/sentry make build push
  # if not
  make build
  ```

- ```shell
  # for help
  docker run \
  --rm ${REPOSITORY} \
  --help
  # output will useful in later
  Commands:
    cleanup      Delete a portion of trailing data based on...
    config       Manage runtime config options.
    consumer
    createuser   Create a new user.
    devserver    Starts a lightweight web server for...
    devservices  Manage dependent development services...
    django       Execute Django subcommands.
    exec         Execute a script.
    export       Exports core metadata for the Sentry...
    files        Manage files from filestore.
    help         Show this message and exit.
    import       Imports data from a Sentry export.
    init         Initialize new configuration directory.
    permissions  Manage Permissions for Users.
    plugins      Manage Sentry plugins.
    queues       Manage Sentry queues.
    repair       Attempt to repair any invalid data.
    run          Run a service.
    shell        Run a Python interactive interpreter.
    start        DEPRECATED see `sentry run` instead.
    tsdb         Tools for interacting with the time series...
    upgrade      Perform any pending database migrations and...
  ```

- ```shell
  #Redis
  docker run \
    --detach \
    --name sentry-redis \
    redis:3.2-alpine
   
  #PostgreSQL
  docker run \
    --detach \
    --name sentry-postgres \
    --env POSTGRES_PASSWORD=secret \
    --env POSTGRES_USER=sentry \
    postgres:9.5
  # Outbound Email
  docker run \
    --detach \
    --name sentry-smtp \
    tianon/exim4
  ```

- ```shell
  #Get a secret-key
  docker run \
    --rm ${REPOSITORY} \
    config generate-secret-key
  # ${REPOSITORY} corresponds to the name used when building your image in the previous step.
  ```

- ```shell
  # Running Migrations
  docker run \
  --link sentry-redis:redis \
  --link sentry-postgres:postgres \
  --link sentry-smtp:smtp \
  --env SENTRY_SECRET_KEY=${SENTRY_SECRET_KEY} \
  --rm -it ${REPOSITORY} upgrade
  ```

- ```shell
  # The base for running commands will look something like:
  docker run \
    --detach \
    --link sentry-redis:redis \
    --link sentry-postgres:postgres \
    --link sentry-smtp:smtp \
    --env SENTRY_SECRET_KEY=${SENTRY_SECRET_KEY} \
    ${REPOSITORY} \
    <command>
  ```

- ```shell
  # start with web gui
  docker run \
    --detach \
    --link sentry-redis:redis \
    --link sentry-postgres:postgres \
    --link sentry-smtp:smtp \
    --publish 9000:9000 \
    --env SENTRY_SECRET_KEY=${SENTRY_SECRET_KEY} \
    ${REPOSITORY} \
    run web
  ```

- ```shell
  # Run periodic task dispatcher
  docker run \
    --detach \
    --link sentry-redis:redis \
    --link sentry-postgres:postgres \
    --link sentry-smtp:smtp \
    --env SENTRY_SECRET_KEY=${SENTRY_SECRET_KEY} \
    ${REPOSITORY} \
    sentry run cron
  ```

- ```shell
  # Run background worker instance.
  docker run \
    --detach \
    --link sentry-redis:redis \
    --link sentry-postgres:postgres \
    --link sentry-smtp:smtp \
    --env SENTRY_SECRET_KEY=${SENTRY_SECRET_KEY} \
    ${REPOSITORY} \
    sentry run worker
  ```

