FROM node:23 AS builder

WORKDIR /usr/src/app
COPY . .

RUN yarn install
RUN yarn build

FROM nginx
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
COPY --from=builder /usr/src/app/build /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /var/run/nginx && \
  chmod -R 755 /usr/share/nginx/html && \
  chown -R appuser:appgroup /usr/share/nginx/html && \
  chown -R appuser:appgroup /var/cache/nginx /var/run /etc/nginx && \
  chmod -R 755 /var/run/nginx

EXPOSE 80

USER appuser

ENTRYPOINT [ "nginx", "-g", "daemon off;" ]