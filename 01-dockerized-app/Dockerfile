FROM golang:1.25-alpine AS builder
LABEL authors="rbt"

WORKDIR /app
COPY go.mod go.sum* ./
RUN go mod download

COPY . .
RUN GO_ENABLED=0 GOOS=linux go build -o myapp main.go

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /app
COPY --from=builder /app/myapp .
EXPOSE 8080
CMD ["./myapp"]
