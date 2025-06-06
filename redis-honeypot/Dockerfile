# Stage 1: Build the binary
FROM golang:1.20-alpine AS builder

# Install git
RUN apk add --no-cache git

# Set workdir
WORKDIR /app

# Clone the repo
RUN git clone https://github.com/cypwnpwnsocute/RedisHoneyPot.git

# Set workdir to the repo
WORKDIR /app/RedisHoneyPot

# Download Go dependencies
RUN go mod download

# Build the binary - using go build without specifying files to include all necessary files
RUN go build -o RedisHoneyPot

# Stage 2: Run the binary
FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/RedisHoneyPot/RedisHoneyPot .
COPY --from=builder /app/RedisHoneyPot/redis.conf .

# Create log directory
RUN mkdir -p /app/logs

EXPOSE 6379

CMD ["sh", "-c", "./RedisHoneyPot -addr 0.0.0.0:6379 -proto tcp -num 1 > logs/redis.log 2>&1"]