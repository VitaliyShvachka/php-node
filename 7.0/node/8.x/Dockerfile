FROM php:7.0

RUN apt-get update && apt-get install -y zip sshpass libpng-dev wget curl jq gnupg unzip git msmtp-mta openssh-client --no-install-recommends && rm -r /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/ \
    && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer
    
RUN curl -sSLo phpunit.phar https://phar.phpunit.de/phpunit-old.phar \
    && chmod 755 phpunit.phar \
    && mv phpunit.phar /usr/local/bin/ \
    && ln -s /usr/local/bin/phpunit.phar /usr/local/bin/phpunit
    
# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs build-essential

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update && apt-get install yarn
    
RUN npm install -g pngquant-bin --allow-root --unsafe-perm=true
RUN npm install -g @angular/cli
RUN npm install -g cross-env

RUN apt-get install -y rsync

RUN rm -r /var/lib/apt/lists/*

COPY msmtprc /etc/
COPY entrypoint.sh /entrypoint.sh
#ENTRYPOINT ["/entrypoint.sh"]
CMD ["php", "-a"]
