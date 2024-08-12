ARG BUILD_ARCH
ARG BUILD_VERSION
ARG BUILD_BASE_IMAGE=zabbix/zabbix-agent2:alpine-latest

FROM ${BUILD_BASE_IMAGE} as builder

FROM alpine

LABEL maintainer "Philipp Schmitt <philipp@schmitt.co>"

ENV LANG C.UTF-8

# Install requirements for add-on
RUN apk add --no-cache jq zabbix-agent2 && \
    addgroup -g 102 docker && \
    addgroup zabbix docker && \
    mkdir -p /etc/zabbix/zabbix_agent2.d/plugins.d

# Copy zabbix-agent2 plugins
COPY --from=builder ["/usr/sbin/zabbix-agent2-plugin", "/usr/sbin/zabbix-agent2-plugin"]

# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
