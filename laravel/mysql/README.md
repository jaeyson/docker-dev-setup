this is for persistent `mysql` storage

if you dont want persistent storage, comment volumes:
```yml
mysql:
  image: mysql:5.7.29
  container_name: mysql
  restart: unless-stopped
  tty: true
  volumes:      <-- comment this!
    - ./mysql:/var/lib/mysql      <-- comment this!
  ports:
    - "3306:3306"
```
