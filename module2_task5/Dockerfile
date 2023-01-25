FROM golang:1.15.8-buster
WORKDIR /app
COPY . .
RUN apt-get update && apt-get install -y make wget
RUN wget https://github.com/gohugoio/hugo/releases/download/v0.109.0/hugo_extended_0.109.0_linux-amd64.deb
RUN dpkg -i hugo_extended_0.109.0_linux-amd64.deb
RUN rm -f hugo_extended_0.109.0_linux-amd64.deb
CMD ["./", "setup.sh"]