### Elixir Docker dev setup

```plaintext
Elixir/
├── app/
│   ├── lib/
│   ├── .formatter.exs
│   ├── mix.exs
│   └── other elixir dir/
├── .env.example
├── .dockerignore
├── .gitattributes
├── .gitignore
├── docker-compose.yml
└── elixir.dockerfile
```

## env

```bash
cp .env.example .env && source $_
```

## build

```bash
docker-compose build && docker-compose up -d

# check if it is running
docker ps
```

## create elixir project

```bash
# create app/ folder for elixir project
mkdir app && cd $_

# add Elixir project
docker exec -it app mix new . <APP_NAME>

# add Phoenix project
docker exec -it app mix phx.new . --app <APP_NAME>

# get deps
docker exec -it app mix deps.get

# if you're getting request failed (:timeout)
docker exec -it -e HEX_HTTP_CONCURRENCY=1 -e HEX_HTTP_TIMEOUT=120 app mix deps.get

# install npm deps (inside app dir)
docker exec -it app npm install --prefix ./assets && \
docker exec -it app node ./assets/node_modules/webpack/bin/webpack.js --mode development

# ecto.create && migrate
docker exec -it app mix ecto.create
docker exec -it app mix ecto.migrate

# run server
docker exec -it app mix phx.server

# (optional) use API v2 (ie resource limits)
docker-compose --compatibility up
```

## test

```bash
# should be inside app/ folder before running command
docker exec -it app mix test
```

## existing project

Same thing as creating new project: only you change the path according to your dir:

```yaml
# docker-compose.yml

# from this
  app:
    volumes:
      - ./app:/home/elixiruser/app

# to this (example)
  app:
    volumes:
      - ./:/home/elixiruser/app

# or this (example)
  <DIR_NAME>:
    volumes:
      - ./<DIR_NAME>:/home/elixiruser/app
```

## limiting resources

Currently it's using `256mb` of memory (limit), update the settings at `docker-compose.yml`

## `CSRF tokens do not match`

if it says `csrf tokens do not match` on pgadmin, try clearing cookies or use incognito.

## other useful commands

```bash
# check ip of running container
docker inspect <CONTAINER_NAME> | grep IPAddress

# runtime metrics of a container
docker stats <CONTAINER_NAME>

# list open ports
sudo lsof -i -P -n | grep LISTEN
```
