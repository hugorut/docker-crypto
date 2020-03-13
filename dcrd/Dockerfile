FROM golang:1.12

WORKDIR /go/src/github.com/decred/

RUN git clone https://github.com/decred/dcrd.git \
    && cd dcrd \
    && CGO_ENABLED=0 GOOS=linux GO111MODULE=on go install . ./cmd/...

FROM alpine:3.10.1

RUN apk add --no-cache ca-certificates
COPY --from=0 /go/bin/* /bin/

EXPOSE 9108 9109

ENTRYPOINT [ "dcrd" ]