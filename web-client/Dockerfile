FROM node:23-alpine as build

WORKDIR /app
COPY . /app

EXPOSE 3000

RUN yarn install
RUN yarn build

CMD ["yarn", "start"]






