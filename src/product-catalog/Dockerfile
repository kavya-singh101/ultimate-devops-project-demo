FROM golang:1.23.10-alpine3.19 AS builder

WORKDIR /usr/src/app

COPY . .

RUN go mod download

# Compile Go binary
RUN go build -o product-catalog ./

FROM alpine:3.19 AS release

WORKDIR /usr/src/app

COPY ./products ./products
COPY --from=builder /usr/src/app/product-catalog ./

ENV PRODUCT_CATALOG_PORT=8088

#EXPOSE ${PRODUCT_CATALOG_PORT}

ENTRYPOINT ["./product-catalog"]

