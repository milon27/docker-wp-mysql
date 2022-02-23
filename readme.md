## Setup wordpress with docker and docker-compose 


>> docker-compose.yml

```yml
version: '3'

# services (root label)
services:
  wp:
    depends_on:
      - db
    image: wordpress:latest
    restart: always
    ports:
      - "3000:80"
    environment:
      - WORDPRESS_DB_HOST=db:3306
      - WORDPRESS_DB_USER=milon27
      - WORDPRESS_DB_PASSWORD=myPassWord
      - WORDPRESS_DB_NAME=wp_db
    volumes:
      - ./:/var/www/html
  db:
    container_name: mysql_db
    image: mariadb:10.7
    restart: always
    environment:
      - MYSQL_USER=milon27
      - MYSQL_PASSWORD=myPassWord
      - MYSQL_ROOT_PASSWORD=myPassWord
      - MYSQL_DATABASE=wp_db
    volumes:
      - mysql_vol:/var/lib/mysql

#volumes(root label)
volumes:
  mysql_vol: {}

```