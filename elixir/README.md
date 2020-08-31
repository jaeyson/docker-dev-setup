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

build

```bash
docker-compose build
```

create elixir project

```bash
# create app/ folder for elixir project
mkdir app && cd $_

docker-compose run --rm app mix new . --app <APP_NAME>
```

test

```bash
# should be inside app/ folder before running command

docker-compose run --rm app mix test
```

