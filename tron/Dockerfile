FROM frolvlad/alpine-java:jdk8-full as runtime

ENV TRON_VERSION=3.6.2 TRON_PATH=/opt/tron
WORKDIR ${TRON_PATH}

USER root

RUN apk update \
    && apk -U upgrade \
    && apk add --no-cache --update libstdc++ curl ca-certificates curl \
    && update-ca-certificates --fresh \
    && rm -rf /var/cache/apk/* \
    && mkdir -p $TRON_PATH/data

ADD logback.xml logback.xml

RUN curl -LO https://raw.githubusercontent.com/tronprotocol/tron-deployment/master/main_net_config.conf \
    && curl -LO https://github.com/tronprotocol/java-tron/releases/download/Odyssey-v$TRON_VERSION/FullNode.jar

EXPOSE 8090 18888 50051
ENTRYPOINT [ "java", "-Xms256m", "-Xmx4096m", "-jar", "FullNode.jar", "-c", "main_net_config.conf", "--log-config", "logback.xml", "--output-directory", "$TRON_PATH/data"]