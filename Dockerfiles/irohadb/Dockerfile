FROM mysql:5.7

LABEL maintainer="hoge@example.com"

WORKDIR /tmp
COPY initdb.sql /docker-entrypoint-initdb.d/

# for Debug
#RUN rm /etc/mysql/mysql.conf.d/mysqld.cnf 
#COPY mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3306

CMD ["mysqld"]
