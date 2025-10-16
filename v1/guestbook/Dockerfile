# Build Stage
FROM golang:1.18 AS builder

WORKDIR /app

COPY main.go .
COPY public/ ./public/

RUN go mod init guestbook
RUN go mod tidy
RUN go build -o guestbook main.go

RUN go build main.go

#Final Stage
FROM ubuntu:18.04
COPY --from=builder /app/guestbook .
COPY --from=builder /app/public ./public
COPY public/ ./public/

WORKDIR /app
CMD ["./guestbook"]
EXPOSE 3000
