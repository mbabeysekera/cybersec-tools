FROM golang:alpine AS builder

RUN apk add --no-cache git ca-certificates

WORKDIR /app
RUN go install github.com/OJ/gobuster/v3@latest

FROM alpine:3.24

# Install ca-certificates to allow HTTPS scanning
RUN apk add --no-cache ca-certificates
RUN addgroup -S appgroup \
    && adduser -S appuser -G appgroup
COPY --from=builder /go/bin/gobuster /usr/local/bin/gobuster

USER appuser

ENTRYPOINT [ "gobuster" ]