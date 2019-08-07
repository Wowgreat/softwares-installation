### 官方推荐安装方法

- ```shell
  git clone https://github.com/getsentry/onpremise.git
  
  REPOSITORY={yorprivateregistry}/sentry make build push
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
  docker run --rm -it ${REPOSITORY} upgrade
  ```

- ```shell
  # start without the web gui
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