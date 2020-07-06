FROM golang:1.14-alpine

ENV INSTALL_DIR /opt/gnmi-gateway

WORKDIR "${INSTALL_DIR}"
COPY . "${INSTALL_DIR}"

RUN apk add --update make gcc g++ git openssl
RUN make build
RUN make tls
RUN ./gnmi-gateway -version

CMD ["./gnmi-gateway", \
    "-TargetJSONFile=./targets.json", \
    "-EnableGNMIServer", \
    "-EnablePrometheusExporter", \
    "-OpenConfigDirectory=./oc-models/", \
    "-ServerTLSCert=server.crt", \
    "-ServerTLSKey=server.key"]