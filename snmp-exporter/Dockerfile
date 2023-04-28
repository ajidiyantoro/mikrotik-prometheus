FROM alpine

LABEL maintainer="ajidiyantoro@gmail.com"
LABEL version="1.0"

ENV snmp_exporter_version 0.21.0

RUN adduser -s /bin/false -D -H prometheus \
    && apk update \
    && apk --no-cache add curl \
    && curl -LO https://github.com/prometheus/snmp_exporter/releases/download/v${snmp_exporter_version}/snmp_exporter-${snmp_exporter_version}.linux-amd64.tar.gz \
    && tar -xvzf snmp_exporter-${snmp_exporter_version}.linux-amd64.tar.gz \
    && mkdir -p /etc/snmp_exporter \
    && cp snmp_exporter-${snmp_exporter_version}.linux-amd64/snmp_exporter /usr/local/bin/ \
    && cp snmp_exporter-${snmp_exporter_version}.linux-amd64/snmp.yml /etc/snmp_exporter/ \
    && rm -rf snmp_exporter-${snmp_exporter_version}.linux-amd64* \
    && chown prometheus:prometheus /usr/local/bin/snmp_exporter \
    && chown -R prometheus:prometheus /etc/snmp_exporter \
    && apk del curl

VOLUME /etc/snmp_exporter

ENTRYPOINT /usr/local/bin/snmp_exporter \ 
    --config.file /etc/snmp_exporter/snmp.yml 

EXPOSE 9116