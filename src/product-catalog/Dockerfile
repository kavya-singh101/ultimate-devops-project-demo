FROM golang:1.22-alpine AS builder

WORKDIR usr/src/app

COPY . .

RUN go mod download

#product-catalog is a custom made folder in usr/src/app
RUN go build -o product-catalog ./

FROM alpine AS release

WORKDIR usr/src/app

# it is taking data from the product folder
COPY ./products ./products

COPY --from=builder /usr/src/app ./

ENV PRODUCT_CATALOG_PORT=8088

ENTRYPOINT ["./product-catalog"]
