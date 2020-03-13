FROM ubuntu:18.04

ENV LANGUAGE=C.UTF-8 LANG=C.UTF-8 LC_ALL=C.UTF-8 DEBIAN_FRONTEND=noninteractive RIPPLE_VERSION=1.3.1

COPY entrypoint /entrypoint.sh

RUN rm -rf /var/lib/apt/lists/* \
    && rm /var/cache/apt/*.bin \
    && apt-get update --fix-missing -y  && \
    apt-get install ssh openssl nano -y && \
    cd /tmp && \
    wget https://repos.ripple.com/repos/rippled-deb/pool/stable/rippled_$RIPPLE_VERSION-1_amd64.deb && \
    dpkg -i rippled_$RIPPLE_VERSION-1_amd64.deb && \
    rm -rf /var/lib/apt/lists/* && \
    export PATH=$PATH:/opt/ripple/bin/ && \
    chmod +x /entrypoint.sh && \
    echo '#!/bin/bash' > /usr/bin/server_info && echo '/entrypoint.sh server_info' >> /usr/bin/server_info && \
    chmod +x /usr/bin/server_info \
    && ln -s /opt/ripple/bin/rippled /usr/bin/rippled

COPY rippled.cfg /etc/opt/ripple/rippled.cfg

EXPOSE 80 443 5005 6006 51235

ENTRYPOINT [ "/entrypoint.sh" ]
