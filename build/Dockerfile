# syntax=docker/dockerfile:1

FROM golang:1.17.3-alpine3.13 as build

LABEL maintainer="Franklin <devsecfranklin@duck.com>"
LABEL org.opencontainers.image.source = "https://github.com/devsecfranklin/peirates"
LABEL org.opencontainers.image.description="Peirates, a Kubernetes penetration tool"
LABEL org.opencontainers.image.licenses=GPLv2

ARG USER="peirates"
ARG MY_HOME="/usr/local/go/src/peirates"

WORKDIR /usr/local/go/src/peirates

COPY go.mod go.sum ./
RUN go mod download

RUN apk add --no-cache \
  gcc \
  libc-dev
COPY . .
RUN ./build.sh

FROM alpine:3.13

COPY --from=build "/usr/local/go/src/peirates/peirates" /peirates
ENTRYPOINT ["/peirates"]
