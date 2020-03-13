FROM debian:stable-slim

ENV HOME=/bitcoinsv USER_ID=1000 GROUP_ID=1000 BSV_VERSION=0.2.1

RUN groupadd -g ${GROUP_ID} bitcoinsv \
  && useradd -u ${USER_ID} -g bitcoinsv -s /bin/bash -m -d /bitcoinsv bitcoinsv \
  && set -x \
  && apt-get update -y \
  && apt-get install -y curl \
  && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
  && curl -sL https://download.bitcoinsv.io/bitcoinsv/${BSV_VERSION}/bitcoin-sv-${BSV_VERSION}-x86_64-linux-gnu.tar.gz | tar xz --strip=2 -C /usr/local/bin

EXPOSE 8332 8333

WORKDIR /bitcoinsv
COPY bitcoin.conf .bitcoin/bitcoin.conf

ENTRYPOINT ["bitcoind"]