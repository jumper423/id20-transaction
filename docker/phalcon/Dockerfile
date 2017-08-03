FROM phalconphp/php-fpm:7

RUN curl -s https://packagecloud.io/install/repositories/phalcon/nightly/script.deb.sh | sudo bash
RUN apt-get update
RUN apt-get install -y php7.0-phalcon

WORKDIR /root
RUN rm -rf /usr/bin/phalcon
RUN git clone git://github.com/phalcon/phalcon-devtools.git /root/phalcon-devtools
RUN ln -s /root/phalcon-devtools/phalcon.php /usr/bin/phalcon
RUN chmod ugo+x /usr/bin/phalcon

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

RUN openssl genrsa -out private.key 1024
RUN openssl rsa -in private.key -pubout -out public.key

RUN echo "xdebug.remote_autostart=on" >> /etc/php/7.0/fpm/conf.d/20-xdebug.ini

COPY xdebug.ini /etc/php/7.0/mods-available/xdebug.ini
#RUN echo "xdebug.remote_host="`/sbin/ip route|awk '/default/ { print $3 }'` >> /etc/php/7.0/mods-available/xdebug.ini

#RUN echo "xdebug.remote_host=192.168.99.100" >> /etc/php/7.0/fpm/conf.d/20-xdebug.ini
#RUN echo "xdebug.remote_host=192.168.99.100" >> /etc/php/7.0/cli/conf.d/20-xdebug.ini
#RUN echo "extension=mongo.so" >> /etc/php/7.0/fpm/php.ini
RUN echo "nameserver 8.8.8.8" >> /etc/resolv.conf
RUN cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime

#==================
# Chrome webdriver
#==================
ARG CHROME_DRIVER_VERSION=2.29
RUN wget --no-verbose -O /tmp/chromedriver_linux64.zip https://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip \
  && rm -rf /opt/selenium/chromedriver \
  && unzip /tmp/chromedriver_linux64.zip -d /opt/selenium \
  && rm /tmp/chromedriver_linux64.zip \
  && mv /opt/selenium/chromedriver /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION \
  && chmod 755 /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION \
  && ln -fs /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION /usr/bin/chromedriver

WORKDIR /app

RUN apt-get install -y nodejs
RUN apt-get install -y npm
RUN npm install pm2 -g

WORKDIR /app

RUN ln -fs /usr/bin/nodejs /usr/local/bin/node

RUN echo "date.timezone = Europe/Moscow" >> /etc/php/7.0/cli/php.ini
RUN echo "date.timezone = Europe/Moscow" >> /etc/php/7.0/fpm/php.ini

#CMD pm2 start
CMD bash