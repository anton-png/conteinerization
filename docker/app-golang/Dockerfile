FROM golang:1.20.5-alpine3.17
RUN apk add --no-cache git

RUN mkdir -p /usr/src/app/tmp
WORKDIR /usr/src/app

RUN git clone https://github.com/adterskov/geekbrains-conteinerization.git ./tmp && \ 
    cp ./tmp/homework/2.docker/golang/* ./ && \
    rm -rf ./tmp

RUN go mod download && go mod verify

RUN CGO_ENABLED=0 GOOS=linux go build -v -o /usr/local/bin/app-go

EXPOSE 8080

CMD ["app-go"]
