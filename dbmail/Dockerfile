FROM jprjr/debian-base:wheezy

RUN export DEBIAN_FRONTEND=noninteractive && \
    echo "deb http://debian.nfgd.net/debian/ wheezy main" > /etc/apt/sources.list.d/dbmail.list && \
    apt-get update && \
    apt-get install -y --force-yes dbmail

RUN mkdir -p /opt/dbmail && \
    mkdir -p /etc/s6/dbmail-imapd && \
    mkdir -p /etc/s6/dbmail-httpd && \
    mkdir -p /etc/s6/dbmail-lmtpd && \
    ln -s /bin/true /etc/s6/dbmail-imapd/finish && \
    ln -s /bin/true /etc/s6/dbmail-httpd/finish && \
    touch /etc/s6/dbmail-httpd/down && \
    ln -s /bin/true /etc/s6/dbmail-lmtpd/finish && \
    touch /var/run/dbmail-imapd.pid && \
    touch /var/run/dbmail-lmtpd.pid && \
    touch /var/run/dbmail-httpd.pid && \
    chown nobody:nogroup /var/run/dbmail-imapd.pid && \
    chown nobody:nogroup /var/run/dbmail-lmtpd.pid && \
    chown nobody:nogroup /var/run/dbmail-httpd.pid

ADD dbmail-imapd.run /etc/s6/dbmail-imapd/run
ADD dbmail-imapd.setup /etc/s6/dbmail-imapd/setup
ADD dbmail-httpd.run /etc/s6/dbmail-httpd/run
ADD dbmail-httpd.setup /etc/s6/dbmail-httpd/setup
ADD dbmail-lmtpd.run /etc/s6/dbmail-lmtpd/run
ADD dbmail-lmtpd.setup /etc/s6/dbmail-lmtpd/setup
ADD conf/dbmail.conf.mysql /opt/dbmail/dbmail.conf.mysql
ADD conf/create_tables.mysql /opt/dbmail/create_tables.mysql

EXPOSE 24
EXPOSE 143
EXPOSE 993
EXPOSE 41380
