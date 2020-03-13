FROM debian:stable-slim

ENV LITECOIN_VERSION=0.17.1

RUN useradd -r litecoin \
  && apt-get update -y \
  && apt-get install -y curl gnupg \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
  && curl -O https://download.litecoin.org/litecoin-${LITECOIN_VERSION}/linux/litecoin-${LITECOIN_VERSION}-x86_64-linux-gnu.tar.gz \
  && tar --strip=2 -xzf *.tar.gz -C /usr/local/bin \
  && rm *.tar.gz \
  && mkdir -p "/root/.litecoin" 

COPY litecoin.conf /root/.litecoin/litecoin.conf

EXPOSE 9332 9333 19332 19333 19444

ENTRYPOINT ["litecoind"]