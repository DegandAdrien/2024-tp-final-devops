FROM node:23-alpine as build

WORKDIR /app
COPY . /app

RUN yarn install
RUN yarn build

FROM node:23-alpine
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app

COPY --from=build /app/ .

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 3000

CMD ["yarn", "start"]






