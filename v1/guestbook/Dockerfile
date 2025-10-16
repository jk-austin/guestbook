# use Go as the parent image
FROM golang:1.18 AS builder

# set the WORKDIR
WORKDIR /app

# copy all app files to the working directory
COPY main.go .
COPY public/ ./public/

RUN go mod init guestbook
RUN go mod tidy
RUN go build -o guestbook main.go

FROM ubuntu:18.04

WORKDIR /app

COPY --from=builder /app/guestbook .
COPY --from=builder /app/public ./public

# Make port 3000 available to the world outside this container
EXPOSE 3000

CMD ["./guestbook"]
