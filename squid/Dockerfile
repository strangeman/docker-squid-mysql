FROM sameersbn/squid:latest
MAINTAINER doublic@gmail.com

#install squidguard and perl mysql libs
RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y squidguard \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y libdbd-mysql-perl libdbi-perl \
 && rm -rf /var/lib/apt/lists/*

#download fresh shallalist database and unpack it for squidguard
RUN wget http://www.shallalist.de/Downloads/shallalist.tar.gz \
 && mkdir -p /var/lib/squidguard/db/shallalist \
 && tar -xzf shallalist.tar.gz -C /var/lib/squidguard/db/shallalist \
 && rm shallalist.tar.gz \
 && chown -R proxy:proxy /var/lib/squidguard/db

#copy squidGuard config and build database
COPY squidGuard.conf /etc/squidguard/squidGuard.conf
COPY db /var/lib/squidguard/db
RUN chown -R proxy:proxy /var/lib/squidguard/db
RUN sudo -u proxy squidGuard -C all -d -b

#copy squid configs
COPY squid3 /etc/squid3 
RUN chmod +x /etc/squid3/squid_mysql_auth

ENTRYPOINT ["/sbin/entrypoint.sh"]
