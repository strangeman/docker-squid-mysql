FROM mariadb
MAINTAINER doublic@gmail.com

ENV MYSQL_ROOT_PASSWORD=examplepass \
	MYSQL_DATABASE=squid \
	MYSQL_USER=squid \
	MYSQL_PASSWORD=squidpass

#copy auth data
COPY data.sql /docker-entrypoint-initdb.d/data.sql