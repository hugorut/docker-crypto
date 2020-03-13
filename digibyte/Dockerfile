FROM ubuntu:18.04

RUN apt-get update \
    && apt-get -y install curl wget \
    && RELEASE=$(curl --silent "https://api.github.com/repos/digibyte/digibyte/releases/latest" | grep '"tag_name":' | sed -E 's/.*"([^"]+)".*/\1/' | cut -c 2-) \
    && wget https://github.com/digibyte/digibyte/releases/download/v$RELEASE/digibyte-$RELEASE-x86_64-linux-gnu.tar.gz \
    && tar -xzf digibyte-$RELEASE-x86_64-linux-gnu.tar.gz \
    && rm digibyte-$RELEASE-x86_64-linux-gnu.tar.gz \
    && chmod +x ./digibyte-$RELEASE/bin/digibyted \
    && mv ./digibyte-$RELEASE/bin/digibyted /usr/bin/digibyted \
    && rm -rf ./digibyte-$RELEASE \
    && mkdir -p /root/.digibyte/data

ADD digibyte.conf /root/.digibyte/digibyte.conf

EXPOSE 12024 14022

ENTRYPOINT ["digibyted","-conf=/root/.digibyte/digibyte.conf","-datadir=/root/.digibyte/data"]