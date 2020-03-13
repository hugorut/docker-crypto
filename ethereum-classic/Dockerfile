FROM golang:1.12-alpine as builder
RUN apk update && apk add git make g++ gcc musl-dev \
    && git clone https://github.com/ethereumproject/go-ethereum \
    && cd ./go-ethereum && make cmd/geth

FROM alpine:latest

RUN apk add --no-cache ca-certificates
COPY --from=builder /go/go-ethereum/bin/geth /usr/local/bin/

EXPOSE 8545 8546 8547 30303 30303/udp

ENTRYPOINT ["geth"]