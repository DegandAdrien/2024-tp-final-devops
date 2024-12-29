FROM golang:1.23 AS builder
WORKDIR /usr/src/myapp
COPY . /usr/src/myapp

RUN go build
RUN mkdir /bin/app
RUN mv vote-api /bin/app

FROM ubuntu:latest
RUN apt-get update && apt-get install -y ca-certificates adduser
RUN addgroup --system appgroup && adduser --system --ingroup appgroup appuser
COPY --from=0 /bin/app /bin/app
ENV PG_URL="postgres://user:password@host.docker.internal:5432/postgres?sslmode=disable"
EXPOSE 8080
RUN chown -R appuser:appgroup /bin/app
USER appuser
CMD ["/bin/app/vote-api"]