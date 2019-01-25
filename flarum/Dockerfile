FROM debian

EXPOSE 8888
ENV DB_SERVER=mariadb
ENV DB_NAME=flarum
ENV DB_USER=flarum
ENV DB_PASSWORD=flarum1234

RUN apt update \
 && apt install apt-transport-https lsb-release ca-certificates wget -y \
 && wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
 && sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list' \
 && apt update \
 && apt install composer php7.2 nginx unzip monit -y \
 && apt install php7.2-dom php7.2-gd php7.2-json php7.2-mbstring php7.2-mysql php7.2-tokenizer php7.2-fpm php7.2-curl -y \
 && mkdir /run/php \
 && mkdir /fr 
 RUN composer create-project flarum/flarum /fr --stability=beta
 RUN chown www-data.www-data /fr && chown www-data.www-data /fr/storage && chown www-data.www-data /fr/public/assets

ADD root /
RUN chmod 0700 /etc/monitrc
CMD [ "/usr/bin/monit -I" ]
