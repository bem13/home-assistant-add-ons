ARG BUILD_FROM

FROM $BUILD_FROM

MAINTAINER Bert Roos

ARG BUILD_ARCH
ARG BUILD_FROM

COPY run.sh /
RUN chmod a+x /run.sh

RUN FILEBEAT_VERSION=9.3.0; \
    FILEBEAT_ARCH="${BUILD_ARCH}"; \
    if [ "${BUILD_ARCH}" = "aarch64" ]; then FILEBEAT_ARCH="arm64"; fi; \
    if [ "${BUILD_ARCH}" = "amd64" ]; then FILEBEAT_ARCH="x86_64"; fi; \
    curl https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-${FILEBEAT_ARCH}.tar.gz -o filebeat.tar.gz && \
    tar xzvf filebeat.tar.gz && \
    rm filebeat.tar.gz && \
    mv filebeat-${FILEBEAT_VERSION}-linux-${FILEBEAT_ARCH} /filebeat && \
    cd /filebeat && \
    cp filebeat /usr/bin

WORKDIR /filebeat/

CMD [ "/run.sh" ]
