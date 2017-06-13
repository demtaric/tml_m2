FROM ubuntu:16.04

RUN apt-get update -y --fix-missing

# Install tools
RUN apt-get install -y \
    software-properties-common \
    python-software-properties \
    net-tools \
    vim

# Add nginx mainline Repository
RUN add-apt-repository ppa:nginx/development

RUN apt-get update && apt-get -y upgrade

RUN apt-get install -y ca-certificates ssl-cert nginx

COPY config/bobcat.dev /etc/nginx/sites-available/

RUN make-ssl-cert generate-default-snakeoil --force-overwrite

RUN ln -s /etc/nginx/sites-available/bobcat.dev /etc/nginx/sites-enabled/bobcat.dev
RUN rm /etc/nginx/sites-enabled/default

RUN usermod -u 1000 www-data

EXPOSE 80
EXPOSE 443
EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
