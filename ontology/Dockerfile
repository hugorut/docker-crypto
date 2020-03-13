FROM alpine:3.10.1

RUN apk add --no-cache ca-certificates curl \
    && curl https://dev.ont.io/ontology_install | sh \
    && mv /ontio/ontology /bin/ontology

EXPOSE 20338 20339 20336 20334

ENTRYPOINT [ "ontology", "--rest" ]