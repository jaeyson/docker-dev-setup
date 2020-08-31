### Elixir Docker dev setup

```plaintext
Elixir/
├── app/
│   ├── lib/
│   ├── .formatter.exs
│   ├── mix.exs
│   └── other elixir dir/
├── .dockerignore
├── docker-compose.yml
└── Dockerfile
```

## Option 1: create a new project

build

```bash
docker-compose build && docker-compose up -d

# check if its running
docker ps
```

create elixir project

```bash
# create app/ folder for elixir project
mkdir app && cd $_

# add Elixir project
docker-compose run --rm app mix new . --app <APP_NAME>

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

test

```bash
# should be inside app/ folder before running command

docker-compose run --rm app mix test
```

## Option 2: existing project

same thing with option 1:

- uncomment `COPY` command in `Dockerfile`

- change the path according to your dir (it doesnt have to be exactly same):

```yaml
# from this
  app:
    volumes:
      - ./app:/home/elixiruser/app

# to this (example)
  app:
    volumes:
      - ./:/home/elixiruser/app
```