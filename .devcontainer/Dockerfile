FROM ubuntu:22.04
LABEL org.opencontainers.image.authors="support@halon.io"

ARG HALON_REPO_USER
ENV HALON_REPO_USER=$HALON_REPO_USER
ARG HALON_REPO_PASS
ENV HALON_REPO_PASS=$HALON_REPO_PASS

RUN apt-get update && apt-get install -y wget gnupg
RUN apt-get update && apt-get install -y apt-transport-https

RUN apt-get update && apt-get install -y git build-essential netcat swaks vim telnet net-tools iputils-ping

RUN wget -qO - https://raw.githubusercontent.com/halon/pgp-keys/master/pgp-keys/7F0A73B5.asc | apt-key add -
RUN echo "deb https://repo.halon.io/ jammy stable" >> /etc/apt/sources.list.d/halon.list
RUN echo "machine repo.halon.io login ${HALON_REPO_USER} password ${HALON_REPO_PASS}" >> /etc/apt/auth.conf

RUN apt-get update && apt-get install -y \
    halon=6.5.5

RUN mkdir /var/log/halon && chown halon:halon /var/log/halon

RUN /usr/bin/install -d /var/run/halon
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH
