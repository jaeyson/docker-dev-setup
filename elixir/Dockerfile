FROM elixir:alpine

# RUN apk add postgresql-client inotify-tools

# RUN mix local.hex --force
# RUN mix local.rebar --force
# RUN mix archive.install hex phx_new --force
RUN addgroup -S -g 1001 elixiruser && \
    adduser -S -u 1000 -G elixiruser elixiruser 

RUN mkdir /app
RUN chown -R elixiruser /app
RUN chgrp -R elixiruser /app

WORKDIR /app
ADD . /app
USER elixiruser
EXPOSE 4000
