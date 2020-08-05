FROM elixir:alpine

RUN apk add postgresql-client inotify-tools

RUN mix local.hex --force
RUN mix local.rebar --force
RUN mix archive.install hex phx_new --force

WORKDIR /app
EXPOSE 4000
