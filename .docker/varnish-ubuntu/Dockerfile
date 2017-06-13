FROM ubuntu:16.04

RUN apt-get update --fix-missing && \
    apt-get install -y varnish

COPY default.vcl /etc/varnish/
RUN chown root:root /etc/varnish/default.vcl

COPY start.sh /start.sh
RUN chown root:root /start.sh
RUN chmod 0777 /start.sh
CMD ["/start.sh"]

EXPOSE 6081
