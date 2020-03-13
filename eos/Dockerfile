FROM ubuntu:18.04

ENV VERSION=1.8.2
RUN apt-get update -y && apt-get install wget -y \
    && wget "https://github.com/EOSIO/eos/releases/download/v${VERSION}/eosio_${VERSION}-1-ubuntu-18.04_amd64.deb" \
    && apt install "./eosio_${VERSION}-1-ubuntu-18.04_amd64.deb" -y \
    && wget "https://eosnodes.privex.io/?config=1" -O p2p-config.ini \
    && mkdir -p /root/.local/share/eosio/nodeos/config \
    && mkdir -p /root/.local/share/eosio/nodeos/data/snapshots \
    && mkdir -p /root/.local/share/eosio/nodeos/data/blocks \
    && cd  /root/.local/share/eosio/nodeos/config \
    && wget https://raw.githubusercontent.com/CryptoLions/EOS-MainNet/master/genesis.json

COPY config.ini /root/.local/share/eosio/nodeos/config/config.ini

RUN cat p2p-config.ini | grep "p2p-peer-address" >> /root/.local/share/eosio/nodeos/config/config.ini

ENTRYPOINT ["nodeos", "--disable-replay-opts", "--delete-all-blocks", "--genesis-json", "/root/.local/share/eosio/nodeos/config/genesis.json"]