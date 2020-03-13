FROM ubuntu:18.04

RUN apt-get update \
    && apt-get -y install curl wget unzip \
    && RELEASE=$(curl --silent "https://api.github.com/repos/bcndev/bytecoin/releases/latest" | grep '"tag_name":' | sed -E 's/.*"([^"]+)".*/\1/' | cut -c 2-) \
    && wget https://github.com/bcndev/bytecoin/releases/download/v$RELEASE/bytecoin-daemons-$RELEASE-linux64.zip \
    && unzip bytecoin-daemons-$RELEASE-linux64.zip \
    && rm bytecoin-daemons-$RELEASE-linux64.zip \
    && rm walletd \
    && rm minerd \
    && chmod +x bytecoind \
    && mv bytecoind /usr/bin/bytecoind 

EXPOSE 8080 8081

ENTRYPOINT ["bytecoind"]