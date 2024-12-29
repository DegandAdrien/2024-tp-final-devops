FROM node:23-alpine as build

WORKDIR /app
COPY . /app

RUN yarn install
RUN yarn build
RUN mv .next/server/pages /app/build

FROM nginx
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
COPY --from=build /app/build /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /var/run/nginx && \
  chmod -R 755 /usr/share/nginx/html && \
  chown -R appuser:appgroup /usr/share/nginx/html && \
  chown -R appuser:appgroup /var/cache/nginx /var/run /etc/nginx && \
  chmod -R 755 /var/run/nginx

EXPOSE 80

USER appuser

ENTRYPOINT ["nginx", "-g", "daemon off;"]



