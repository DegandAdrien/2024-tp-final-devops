FROM node:23 AS builder

WORKDIR /usr/src/app
COPY . /usr/src/app

RUN yarn install
RUN yarn build

FROM nginx
COPY --from=builder /usr/src/app/build /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN chmod -R 755 /usr/share/nginx/html

EXPOSE 80

ENTRYPOINT [ "nginx", "-g", "daemon off;" ]