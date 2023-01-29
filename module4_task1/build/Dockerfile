FROM golang:1.15.8-buster
WORKDIR /app
COPY . .
RUN apt-get update && apt-get install -y make wget
RUN wget https://github.com/gohugoio/hugo/releases/download/v0.109.0/hugo_extended_0.109.0_linux-amd64.deb
RUN dpkg -i hugo_extended_0.109.0_linux-amd64.deb
RUN rm -f hugo_extended_0.109.0_linux-amd64.deb
RUN curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.50.1
ENV NODE_VERSION=16.13.0
RUN apt install -y curl
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
ENV NVM_DIR=/root/.nvm
RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
RUN npm install -g markdownlint-cli
ENV PATH="/bin/markdownlint:${PATH}"
CMD ["./", "setup.sh"]
# binary will be $(go env GOPATH)/bin/golangci-lint
