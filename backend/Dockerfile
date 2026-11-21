
# Stage 1: Build the Go application
FROM golang:1.26-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 go build -o devboard-backend .

# Stage 2: Minimal runtime image
FROM alpine:3.22

WORKDIR /app

RUN adduser -D -u 10001 app

COPY --from=builder --chown=app:app /app/devboard-backend .

USER app

EXPOSE 8080

ENTRYPOINT ["./devboard-backend"]

