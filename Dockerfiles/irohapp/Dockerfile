FROM centos:7
LABEL maintainer="hoge@example.com"

ARG version="0.9.18"
WORKDIR /tmp

# Install wget
RUN yum -y install wget httpd php php-mysql

# Install entrykit 
RUN wget https://github.com/progrium/entrykit/releases/download/v0.4.0/entrykit_0.4.0_linux_x86_64.tgz
RUN tar -xvzf entrykit_0.4.0_linux_x86_64.tgz
RUN rm entrykit_0.4.0_linux_x86_64.tgz
RUN mv entrykit /usr/local/bin/
RUN entrykit --symlink

# cakephp-2.7.11
RUN wget https://github.com/cakephp/cakephp/archive/2.7.11.tar.gz
RUN tar -xvzf 2.7.11.tar.gz
RUN rm 2.7.11.tar.gz
RUN mv cakephp-2.7.11 /var/www/cake

# Install Irohaboard
RUN wget https://github.com/irohasoft/irohaboard/archive/v${version}.tar.gz
RUN tar -xvzf v${version}.tar.gz
RUN rm v${version}.tar.gz
RUN mv /var/www/html /var/www/_html
RUN mv irohaboard-${version} /var/www/html
RUN rm /var/www/html/Config/database.php
COPY conf/database.php.tmpl /var/www/html/Config/

# Copy httpd.conf
RUN rm /etc/httpd/conf/httpd.conf
COPY conf/httpd.conf /etc/httpd/conf/

# Change session management
RUN rm /var/www/html/Config/core.php
COPY conf/core.php /var/www/html/Config/

RUN chown -R apache.apache /var/www

ENTRYPOINT [ \
  "render", \
      "/var/www/html/Config/database.php", \
      "--" \
]

EXPOSE 80
CMD ["apachectl", "-DFOREGROUND"]

