FROM nginx:1.16.0

RUN apt-get update && apt-get install -y vim net-tools

RUN mkdir /etc/ssl/private && chmod 700 /etc/ssl/private
ADD etc/ssl/private/nginx-selfsigned.key /etc/ssl/private/nginx-selfsigned.key
ADD etc/ssl/certs/nginx-selfsigned.crt /etc/ssl/certs/nginx-selfsigned.crt
ADD etc/ssl/certs/dhparam.pem /etc/ssl/certs/dhparam.pem

ADD etc/site.conf /etc/nginx/conf.d/default.conf
ADD bin/* /usr/local/bin/

ENV UPLOAD_MAX_FILESIZE 64M
ENV FPM_HOST php
ENV FPM_PORT 9000
ENV MAGENTO_ROOT /var/www/magento2
ENV MAGENTO_RUN_MODE developer
ENV DEBUG false

RUN ["chmod", "+x", "/usr/local/bin/docker-environment"]

ENTRYPOINT ["/usr/local/bin/docker-environment"]
CMD ["nginx", "-g", "daemon off;"]
