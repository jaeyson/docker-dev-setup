FROM elixir:alpine

ARG UID
ARG GID

RUN $GID=$(id -g) && $UID=$(id -u)

RUN apk add postgresql-client inotify-tools shadow && \
    addgroup -g 1000 -S elixirgroup && \
    adduser -u 1000 -S elixir -G elixirgroup && \
    # usermod -u 1000 www-data && groupmod -g 1000 www-data && \
    mix local.hex --force && \
    mix archive.install hex phx_new --force && \
    mix local.rebar --force

ENV APP_HOME /phoenix
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
RUN chown -R elixir $APP_HOME

USER elixir
VOLUME $APP_HOME
CMD ["mix", "phx.server"]
