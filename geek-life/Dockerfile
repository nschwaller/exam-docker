FROM golang:1.14 AS builder
WORKDIR /app
COPY . .
RUN go build -o geek-life ./app
FROM golang:1.14-alpine
WORKDIR /app
COPY --from=builder /app/geek-life ./geek-life
CMD ["./geek-life"]