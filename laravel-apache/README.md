# Laravel Docker dev setup

```plaintext
Laravel
├── mysql/
├── sql/
│   └── sampledb.sql
├── web_app/
│   ├── app/
│   ├── bootstrap/
│   ├── config/
│   ├── ...
│   └── public/
├── .dockerignore
├── docker-compose.yml
├── Dockerfile
└── README.md
```

## create folder `mysql`, `sql` and for `laravel` if not exist

## if you want to use Laravel template

```bash
git clone https://github.com/laravel/laravel web_app --single-branch --branch master --depth 1 
```

## check config and `.env` file

### note: `DB_HOST` variable is based on container name of db, check also `DB_PASSWORD` etc.

```bash
# go to web_app dir
cd web_app

docker-compose config
```

## build and run (detached)

```bash
docker-compose build && docker-compose up -d
```

## list process

```bash
# list running
docker ps

# list all
docker ps -a
```

## import sql

```bash
docker exec --rm -it mysql bash

mysql -u<USER> -p<PASSWORD> <DB_NAME> < docker-entrypoint-initdb.d/<SQL_FILE>

# exit bash or CTRL + D
exit
```

## install deps

```bash
docker-compose run -rm composer install

docker-compose run --rm artisan key:generate
docker-compose run --rm artisan migrate

docker-compose run --rm npm install
docker-compose run --rm npm run dev
```

once done, visit `localhost:9000`

---

## Laravel The stream or file `/storage/logs/laravel.log` could not be opened: `failed to open stream: Permission denied`

```bash
# go to php container
docker exec -it php bash

# change permissions and group for these folders
chgrp -R www-data storage bootstrap/cache
chmod -R ug+rwx storage bootstrap/cache
```

## All Routes Except Home Result in 404 Error

```bash
# go to php container
docker exec -it php bash

a2enmod rewrite && service apache2 restart
```
