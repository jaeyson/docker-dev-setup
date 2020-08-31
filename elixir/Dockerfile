FROM elixir:alpine

ENV HOMEDIR /home/elixiruser/app

RUN apk add postgresql-client inotify-tools npm

RUN addgroup -S -g 1001 elixiruser && \
    adduser -S -u 1000 -G elixiruser elixiruser

RUN mkdir -p $HOMEDIR
# COPY --chown=elixiruser . $HOMEDIR
WORKDIR $HOMEDIR

USER elixiruser

RUN mix local.hex --force
RUN mix local.rebar --force
RUN mix archive.install hex phx_new --force

EXPOSE 4000
