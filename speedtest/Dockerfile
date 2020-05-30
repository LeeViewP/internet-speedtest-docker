#FROM python:2-alpine
FROM alpine AS builder

# Download QEMU, see https://github.com/docker/hub-feedback/issues/1261
ENV QEMU_URL https://github.com/balena-io/qemu/releases/download/v3.0.0%2Bresin/qemu-3.0.0+resin-arm.tar.gz
RUN apk add curl && curl -L ${QEMU_URL} | tar zxvf - -C . --strip-components 1

FROM  arm32v7/python:2-alpine

# Add QEMU
COPY --from=builder qemu-arm-static /usr/bin

MAINTAINER Lee View lee.view@gmail.com

RUN mkdir -p /app/speedtest/
RUN apk add --update curl
RUN curl https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py -o /app/speedtest/speedtest-cli
RUN chmod +x /app/speedtest/speedtest-cli

ADD scripts/ /app/speedtest/

CMD sh -c /app/speedtest/init_test_connection.sh
