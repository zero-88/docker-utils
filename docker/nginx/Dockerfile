ARG ARGBASH_VERSION=2.10.0
FROM matejak/argbash:$ARGBASH_VERSION as builder

WORKDIR /app
COPY nplet.m4 ./
RUN argbash nplet.m4 -o nplet \
    && chmod +x nplet

FROM alpine:3.12

ARG MAINTAINER="zero88 <sontt246@gmail.com>"

WORKDIR /app

RUN apk add --no-cache curl jq bash \
    && addgroup -S -g 1000 bot \
    && adduser -S -u 1001 -G bot runner \
    && chown -R runner:bot /app

COPY --chown=runner:bot --from=builder /app/nplet ./

USER runner:bot

ENV PATH="/app:${PATH}"

ENTRYPOINT [ "nplet" ]
