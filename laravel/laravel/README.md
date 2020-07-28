### Place your laravel files here

```
.
├── docker-compose.yml
├── Dockerfile
├── laravel/
│   ├── app/
│   ├── bootstrap/
│   ├── config/
│   ├── ...
│   └── public/
├── mysql/
└── nginx/
```

build and run (detached):

```bash
docker-compose build && docker-compose up -d
```

list process:

```bash
# list running
docker ps

# list all
docker ps -a
```

once done, visit `localhost`

