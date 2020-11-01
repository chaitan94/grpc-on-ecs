FROM golang:alpine AS build-env

RUN mkdir /app
WORKDIR /app

COPY go.mod .
COPY go.sum .
RUN apk add git
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o /go/bin/app


FROM scratch

COPY --from=build-env /go/bin/app /go/bin/app
CMD [ "/go/bin/app" ]
