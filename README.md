###Dockerfile for OpenEats with everything except the database.

Here's a basic example of usage with docker-compose:

```yaml
version: '3.1'
services:
  openeats:
    build: ./
    depends_on:
      - mysql
    ports:
      - 80:80
    environment:
      - ALLOWED_HOST=*
      - SUPERUSER_NAME=please-change
      - SUPERUSER_PASSWORD=please-change
      - MYSQL_HOST=mysql
      - MYSQL_PORT=3306
      - MYSQL_DATABASE=openeats
      - MYSQL_USER=root
      - MYSQL_PASSWORD=root
      - MYSQL_ROOT_PASSWORD=root
    volumes:
      - ./docker/volumes/static-files:/code/static-files
      - ./docker/volumes/site-media:/code/site-media

  mysql:
    image: mysql:5.7
    environment:
        - MYSQL_ROOT_PASSWORD=root
        - MYSQL_DATABASE=openeats
        - MYSQL_PASSWORD=root
    volumes:
      - "./docker/volumes/mysql:/var/lib/mysql"
```