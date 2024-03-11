FROM debian:unstable-slim

RUN apt-get update && apt-get install -y \
    nginx \
    build-essential \
    libpcre3 \
    libpcre3-dev \
    zlib1g-dev \
    libssl-dev \
    openssl \
    wget

RUN openssl req -x509 -nodes -days 365 -newkey rsa:3096 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt -subj "/C=US/ST=Denial/L=Springfield/O=Dis/CN=localhost"

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
