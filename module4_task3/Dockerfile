FROM golang:1.15.8-buster
WORKDIR /app
COPY . .
RUN apt-get update && apt-get install -y make wget
RUN wget https://github.com/gohugoio/hugo/releases/download/v0.109.0/hugo_extended_0.109.0_linux-amd64.deb
RUN dpkg -i hugo_extended_0.109.0_linux-amd64.deb
RUN rm -f hugo_extended_0.109.0_linux-amd64.deb
RUN curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.50.1

CMD ["./", "setup.sh"]
# binary will be $(go env GOPATH)/bin/golangci-lint
