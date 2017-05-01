# wordpress-nginx
Nginx container configured for use with Wordpress on php-fpm

```bash
docker pull milanb/wordpress-nginx
```

Can be used in conjunction with [wordpress-sqlite](https://github.com/milanboers/wordpress-sqlite) to provide a full lightweight Wordpress solution.

Example docker-compose.yml for both:
```yaml
version: '2'
services:
    wp:
        image: milanb/wordpress-sqlite
        environment:
            - WP_HOME=https://mysite.com
            - WP_SITEURL=https://mysite.com
        volumes:
            - db:/var/www/db
            - uploads:/var/www/html/wp-content/uploads
        restart: always
    http:
        build: http
        links:
            - wp:wordpress
        volumes_from:
            - wp
        ports:
            - "8081:80"
volumes:
    db:
        external: true
    uploads:
        external: true
```
