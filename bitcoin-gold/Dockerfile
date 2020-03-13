FROM ubuntu:18.04

RUN apt-get update \
    && apt-get -y install wget curl \
    && RELEASE=$(curl --silent "https://api.github.com/repos/BTCGPU/BTCGPU/releases/latest" | grep '"tag_name":' | sed -E 's/.*"([^"]+)".*/\1/' | cut -c 2-) \
    && wget https://github.com/BTCGPU/BTCGPU/releases/download/v$RELEASE/bitcoin-gold-$RELEASE-x86_64-linux-gnu.tar.gz \
    && tar -xzvf bitcoin-gold-$RELEASE-x86_64-linux-gnu.tar.gz \
    && chmod +x bitcoin-gold-$RELEASE/bin/bgoldd \
    && mv ./bitcoin-gold-$RELEASE/bin/bgoldd /usr/bin/bgoldd \
    && mkdir -p /root/.bgold/data

ADD bgold.conf /root/.bgold/bgold.conf

EXPOSE 8338 8332

ENTRYPOINT ["bgoldd", "-conf=/root/.bgold/bgold.conf", "-datadir=/root/.bgold/data"]