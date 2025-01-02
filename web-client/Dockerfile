FROM node:23-alpine as build

WORKDIR /app
COPY . /app

RUN yarn install
RUN yarn build
RUN mv .next/server/pages /app/build

FROM node:23-alpine
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app

COPY --from=build /app/ .

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 3000

CMD ["yarn", "start"]

COPY nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /var/run/nginx && \
  chmod -R 755 /usr/share/nginx/html && \
  chown -R appuser:appgroup /usr/share/nginx/html && \
  chown -R appuser:appgroup /var/cache/nginx /var/run /etc/nginx && \
  chmod -R 755 /var/run/nginx

EXPOSE 80

USER appuser

ENTRYPOINT ["nginx", "-g", "daemon off;"]



