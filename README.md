# Docker Crypto

Config and Dockerfiles needed to run individual blockchain nodes

## Get Started

> Clone the repo.
> Build a coin: e.g.

```
docker build ./litecoin -t litecoin
```

> run the coin with args

```
docker run -u 0 -p 80:9332 --name litecoin -d litecoin:latest -rpcuser=test -rpcpassword=testing`
```

## Supports

Currently this repo supports:

* Bitcoin SV
* Bitcoin Gold
* Digibyte
* EOS
* Litecoin
* NEO
* Ripple
* Bytecoin
* DCRD
* Ontology
* Tron
* NEM
* Ethereum Classic

If you don't see a coin here then it is most likely there is a publically available docker image that is well supported. For example Ethereum/Bitcoin.


