### Elixir Docker dev setup

build

```bash
docker-compose build
```

create elixir project

```bash
# create app/ folder for elixir project
mkdir app && cd $_

docker-compose run --rm phoenix mix new . --app <APP_NAME>
```

test

```bash
# should be inside app/ folder before running command

docker-compose run --rm phoenix mix test
```

