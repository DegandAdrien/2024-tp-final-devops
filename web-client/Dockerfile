FROM node:23-alpine as build

WORKDIR /app
COPY . /app

RUN yarn install
RUN yarn build
RUN mv .next/server/pages /app/build

FROM nginx
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]



