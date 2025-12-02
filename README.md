version: '3.8'

services:
  mysql:
    image: mysql:5.7
    restart: always
    container_name: mysql_container
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpressdb
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppass
    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    restart: always
    container_name: wordpress_container
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: mysql:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppass
      WORDPRESS_DB_NAME: wordpressdb
    depends_on:
      - mysql

volumes:
  mysql_data:
