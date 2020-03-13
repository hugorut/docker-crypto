FROM mcr.microsoft.com/dotnet/core/runtime:2.2

ENV NEOCLI_VERSION 2.10.3
ENV NEOCLI_SHA256 9724D03CA521556E1FEB6F2D77C2C9F35EAB174E7A6E9CCC99B321AD49EA5A89

RUN apt-get update \
    && apt-get install -y screen libleveldb-dev sqlite3 unzip \
    && rm -rf /var/lib/apt/lists/* \
    && curl -sSL -o neo-cli-linux.zip https://github.com/neo-project/neo-cli/releases/download/v$NEOCLI_VERSION/neo-cli-linux-x64.zip \
    && echo "$NEOCLI_SHA256 *neo-cli-linux.zip" | sha256sum -c - \
    && unzip neo-cli-linux.zip \
    && rm -rf neo-cli-linux.zip \
    && cd neo-cli \
    && sed -i "s/127.0.0.1/0.0.0.0/g" ./config.json \
    && curl -sSL -o ApplicationLogs.zip https://github.com/neo-project/neo-plugins/releases/download/v2.10.3/ApplicationLogs.zip \
    && unzip ApplicationLogs.zip \
    && rm -rf ApplicationLogs.zip \
    && curl -sSL -o SimplePolicyPlugin.zip https://github.com/neo-project/neo-plugins/releases/download/v2.10.3/SimplePolicyPlugin.zip \
    && unzip SimplePolicyPlugin.zip \
    && rm -rf SimplePolicyPlugin.zip \
    && curl -sSL -o RpcWallet.zip https://github.com/neo-project/neo-plugins/releases/download/v2.10.2/RpcWallet.zip \
    && unzip RpcWallet.zip \
    && rm -rf RpcWallet.zip

EXPOSE 10331 10332 10333 10334
WORKDIR /neo-cli/data
ENTRYPOINT ["screen","-DmS","node","dotnet","/neo-cli/neo-cli.dll","-r", "--logs"]