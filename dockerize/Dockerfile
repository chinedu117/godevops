FROM golang:latest as builder

ENV APP_HOME /go/src/webserver

WORKDIR /app/
COPY . .

RUN go mod download
RUN go mod verify
RUN go build webserver.go

FROM golang:latest

ENV APP_HOME /go/src/webserver
RUN mkdir -p "$APP_HOME"
WORKDIR "$APP_HOME"
COPY . .
COPY --from=builder "$APP_HOME"/webserver $APP_HOME

EXPOSE 8222
CMD ["./webserver"]
