FROM tscangussu/tini:0.16.1-alpine

LABEL Maintainer="Thiago Cangussu <thiago.cangussu@gmail.com>" \
      Description="PHP-FPM based on Alpine Linux." \
      Version="7.1.9"


# Install packages based on official php-fpm image.
# See https://github.com/docker-library/php.
RUN apk --no-cache add php7-fpm php7-zlib php7-mysqlnd php7-mbstring php7-curl php7-ftp php7-opcache php7-openssl

# Ensure www-data user exists and set proper permissions
RUN set -x \
&& addgroup -g 82 -S www-data \
&& adduser -u 82 -D -S -G www-data www-data

# Docker related php-fpm config. Also sets php-fpm user/group to www-data.
COPY zz-docker.conf /etc/php7/php-fpm.d/

# /srv contains site-specific data which is served by this system.
# See FHS 3.0 spec: http://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch03s17.html
ENV WWW-ROOT /srv/www/html

WORKDIR ${WWW-ROOT}

# Run docker-php-entrypoint after tini has been started as PID 1.
COPY docker-php-entrypoint /usr/local/bin

ENTRYPOINT ["tini", "--", "docker-php-entrypoint"]

EXPOSE 9000

CMD ["php-fpm7"]
