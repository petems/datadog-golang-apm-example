FROM golang:1.21.9-alpine

WORKDIR /app

# Download Go modules
COPY go.mod .
COPY go.sum .
RUN go mod download

# Build
COPY *.go .
RUN go build -o hello-world

EXPOSE 8000

# Run
CMD [ "./hello-world" ]