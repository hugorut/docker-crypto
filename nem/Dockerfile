FROM openjdk:8-slim

ARG NIS_VER=0.6.97

RUN apt-get update && \
  apt-get install -y \
    wget \
    gettext-base \
    && \
  wget http://bob.nem.ninja/nis-$NIS_VER.tgz && \
  tar xzf nis-$NIS_VER.tgz && \
  wget https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64.deb && \
  dpkg -i dumb-init_*.deb && \
  apt-get autoclean && \
  apt-get autoremove -y && \
  rm -rf \
  /nis-*.tgz \
  /dumb-init_*.deb \
  /root/.npm \
  /root/.node-gyp \
  /tmp/* \
  /var/lib/apt/lists/*

COPY ./replace-envvars.sh /package/nis
COPY ./config.properties /package

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8 JAVA_OPTS="-Xms1G -Xmx4G" NEM_NETWORK="mainnet"
EXPOSE 7890 7891 7778

WORKDIR /package/nis

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["bash", "-c", "./replace-envvars.sh && java -Xms1G -Xmx4G -Dnem.network=\"mainnet\" -cp \".:./*:../libs/*\" org.nem.deploy.CommonStarter"]