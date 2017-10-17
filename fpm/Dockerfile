FROM tscangussu/tini:0.16.1-alpine

LABEL Maintainer="Thiago Cangussu <thiago.cangussu@gmail.com>" \
      Description="PHP-FPM based on Alpine Linux." \
      Version="7.1.9"

RUN apk --no-cache add php7-fpm

COPY php7 /etc/php7

ARG ROOT="/srv/www/html"

COPY src ${ROOT}

# Ensure www-data user exists and set proper permissions
RUN set -x \
	&& addgroup -g 82 -S www-data \
  && adduser -u 82 -D -S -G www-data www-data \
  && chown -R www-data:www-data ${ROOT} \
  && chmod -R 755 ${ROOT}

EXPOSE 9000

CMD ["php-fpm7"]
