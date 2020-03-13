FROM ubuntu:18.04

RUN apt-get update \
    && apt-get -y install wget curl \
    && RELEASE=$(curl --silent "https://api.github.com/repos/dogecoin/dogecoin/releases/latest" | grep '"tag_name":' | sed -E 's/.*"([^"]+)".*/\1/' | cut -c 2-) \
    && wget https://github.com/dogecoin/dogecoin/releases/download/v$RELEASE/dogecoin-$RELEASE-x86_64-linux-gnu.tar.gz \
    && tar -xzvf dogecoin-$RELEASE-x86_64-linux-gnu.tar.gz \
    && chmod +x dogecoin-$RELEASE/bin/dogecoind dogecoin-$RELEASE/bin/dogecoin-cli \
    && mv ./dogecoin-$RELEASE/bin/dogecoind /usr/bin/dogecoind \
    && mkdir -p /root/.dogecoin/data

ADD dogecoin.conf /root/.dogecoin/dogecoin.conf

EXPOSE 22555 22556 44555 44556

ENTRYPOINT ["dogecoind", "-conf=/root/.dogecoin/dogecoin.conf", "-datadir=/root/.dogecoin/data"]