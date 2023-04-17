FROM node:16.13.1-alpine AS build

WORKDIR app

COPY . .

RUN npm install; npm i -g npm; npm i; npm run build

FROM nginx AS final

WORKDIR /usr/share/nginx/html

COPY --from=build /app/build .

EXPOSE 3000

CMD ["/bin/sh", "-c", "sed -i 's/listen  .*/listen 3000;/g' /etc/nginx/conf.d/default.conf && exec nginx -g 'daemon off;'"]
