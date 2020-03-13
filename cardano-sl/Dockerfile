FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y bzip2 curl git xz-utils \
    && apt-get clean \
    && rm -fr /var/lib/apt/lists/* \
    && useradd -ms /bin/bash cardano \
    && mkdir /nix && chown cardano /nix \
    && mkdir -p /etc/nix \
    && touch /etc/nix/nix.conf \
    && echo substituters = https://hydra.iohk.io https://cache.nixos.org  > /etc/nix/nix.conf \
    && echo trusted-substituters = >> /etc/nix/nix.conf \
    && echo trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY= >> /etc/nix/nix.conf \
    && echo binary-caches = https://cache.nixos.org https://hydra.iohk.io > /etc/nix/nix.conf \
    && echo binary-cache-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY= >> /etc/nix/nix.conf \
    && echo sandbox = false >> /etc/nix/nix.conf \
    && cat /etc/nix/nix.conf \
    && echo "cardano ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER cardano
ENV USER=cardano

RUN curl https://nixos.org/nix/install | sh \
    && git clone --branch master https://github.com/input-output-hk/cardano-sl.git --branch 3.0.2 /home/cardano/cardano-sl \
    && cd /home/cardano/cardano-sl \
    && . /home/cardano/.nix-profile/etc/profile.d/nix.sh \
    && nix-build -A cardano-sl-node-static --cores 0 --max-jobs 2 --out-link master \
    && . /home/cardano/.nix-profile/etc/profile.d/nix.sh \
    && nix-build -A connectScripts.mainnet.explorer -o connect-explorer-to-mainnet

EXPOSE 8100

ENTRYPOINT ["/home/cardano/cardano-sl/connect-explorer-to-mainnet"]