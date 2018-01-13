FROM golang:1.9-alpine

# Install common packages
RUN apk update && \
    apk upgrade && \
    apk add --no-cache git openssh curl

# Install glide
RUN curl https://glide.sh/get | sh

# Install zb
RUN go-wrapper download jrubin.io/zb && go-wrapper install jrubin.io/zb
