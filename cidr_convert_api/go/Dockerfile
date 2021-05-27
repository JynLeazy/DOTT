FROM golang:alpine3.13

ENV GOPATH=/go:/app

RUN apk add --update git
RUN apk add build-base
RUN apk add entr

WORKDIR /app

RUN go get github.com/gorilla/mux
RUN go get github.com/pkg/errors
RUN go get github.com/stretchr/testify/assert
RUN go get -u golang.org/x/lint/golint
COPY . .

RUN go mod init doot
RUN go mod tidy
RUN go build api.go convert.go
#RUN go run api.go convert.go
RUN golint convert.go convert_test.go api.go

RUN go get github.com/t-yuki/gocover-cobertura

# till now, all its good BD

RUN go test -coverprofile=coverage.out 2> error.txt

# COPY . .
# CMD ["ash", "-c", "goop go run api.go convert.go"]
# docker build -t gom .
# docker run -ti -p 8000:8000 gom


