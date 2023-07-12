FROM python:3-alpine
RUN apk add --no-cache git

RUN mkdir -p /usr/src/app/tmp
WORKDIR /usr/src/app

RUN git clone https://github.com/adterskov/geekbrains-conteinerization.git ./tmp && \
    cp ./tmp/homework/2.docker/python/* ./ && \
    rm -rf ./tmp

RUN pip install -r requirements.txt

EXPOSE 8080

CMD [ "flask", "run","--host","0.0.0.0","--port","8080"]
