# Docker Compose - apache
```
version: '3.8'

services:
  php_apache:
    container_name: docker-container
    build: 
      context: .
    ports:
      - "80:80"
    volumes:
      - ./html:/var/www/html
      # - ./sites-enabled:/etc/apache2/sites-enabled
    working_dir: /var/www/html
    restart: unless-stopped

```

# Dockerfile
```
# Dockerfile
FROM php:7.4-apache

# Install additional PHP extensions
RUN apt-get update && \
    apt-get install -y \
    libpq-dev \
    && docker-php-ext-install pdo pdo_mysql mysqli pdo_pgsql

RUN apt-get update && \
    apt-get install -y vim

# Enable Apache mod_rewrite for .htaccess support
RUN a2enmod rewrite
RUN a2enmod session

# Install mysqli extension
# RUN docker-php-ext-install mysqli

# Update the Apache configuration to allow .htaccess overrides
RUN sed -i 's/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

# Install any additional PHP extensions you may need
# For example, if you need the MySQL extension:
# RUN docker-php-ext-install mysqli
# COPY php.ini /usr/local/etc/php/php.ini
# RUN mv /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini
# Expose port 80 to the outside world
EXPOSE 81

# Start Apache in the foreground
CMD ["apache2-foreground"]
```
# file structure 

├── html
│ └── web1
├── Dockerfile
└── docker-compose.yml

# Docker build images
```
docker-compose build
```
# Docker Run 
```
docker-compose up -d
```
# login in docker container
```
docker exec -it <container-name> /bin/bash
```

# restart apache or nginx
```
service apache2 restart
```
```
service nginx restart
```

