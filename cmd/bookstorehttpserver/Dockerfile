FROM golang:1.16-buster AS builder

WORKDIR /app

COPY go.mod ./
COPY go.sum ./
COPY pkg/ ./pkg/

COPY cmd/bookstorehttpserver/main.go ./cmd/bookstorehttpserver/main.go

RUN go build -o /server ./cmd/bookstorehttpserver/main.go

FROM gcr.io/distroless/base-debian10

COPY --from=builder /server /server

EXPOSE 8080

USER nonroot:nonroot

ENTRYPOINT ["/server"]

