FROM php:7.4.7-fpm-alpine

WORKDIR /var/www/html

#RUN docker-php-ext-install pdo pdo_mysql
RUN apk add shadow && usermod -u 1000 www-data && groupmod -g 1000 www-data

#ARG USER=default
#ENV HOME /home/$USER
#
## install sudo as root
#RUN apk add --update sudo
#
## add user
#RUN adduser -D $USER \
#        && echo "$USER ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/$USER \
#        && chmod 0440 /etc/sudoers.d/$USER
#
#USER $USER
#WORKDIR $HOME
#
#CMD echo "User $(whoami) in $PWD with permissions: $(sudo -l)"
