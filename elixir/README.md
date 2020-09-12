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
└── Dockerfile
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
docker-compose run --rm app mix new . <APP_NAME>

# add Phoenix project
docker-compose run --rm app mix phx.new . --app <APP_NAME>

# get deps
docker-compose run --rm app mix deps.get

# create db
docker exec -it db psql -U postgres -c 'create database <DB_NAME>;'

# ecto.create && migrate
docker-compose run --rm app mix ecto.create
docker-compose run --rm app mix ecto.migrate

# install npm deps
docker-compse run --rm app npm install --prefix ./assets

# run server
docker exec -it app mix phx.server
```

## test

```bash
# should be inside app/ folder before running command
docker-compose run --rm app mix test
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

## `CSRF tokens do not match`

if it says `csrf tokens do not match` on pgadmin, try clearing cookies or use incognito.

## other useful commands

```bash
# check ip of running container
docker inspect <CONTAINER_NAME> | grep IPAddress

# list open ports
sudo lsof -i -P -n | grep LISTEN
```
