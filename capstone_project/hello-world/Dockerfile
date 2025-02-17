FROM node:16.13.1-alpine AS build

WORKDIR app

COPY . .

RUN npm install; npm i -g npm; npm i; npm run build

FROM ubuntu

RUN apt-get update  -y \
    && apt-get upgrade -y \ 
    && apt-get install -y \
    ssh \
    sshpass \
    sudo \
    software-properties-common \
    nginx

RUN add-apt-repository --yes --update ppa:ansible/ansible \
    && apt-get install -y ansible

WORKDIR /home/ansible_controller

RUN useradd -rm -d /home/ansible_controller -s /bin/bash -g root -G sudo -u 1001 ansible_controller
RUN echo ansible_controller:12345 | chpasswd
RUN echo "ansible_controller ALL=(ALL:ALL) NOPASSWD: ALL" |  EDITOR="tee -a"  visudo


RUN mkdir -p /home/ansible_controller/.ssh
RUN service ssh start

WORKDIR /usr/share/nginx/html

RUN rm index.html

COPY --from=build app/build .
COPY default.conf ../../../../etc/nginx/conf.d 

EXPOSE 3000
EXPOSE 22

CMD ["/bin/sh", "-c", "service ssh start && exec nginx -g 'daemon off;'"]