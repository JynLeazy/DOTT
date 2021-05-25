pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          image 'golang:alpine3.13'
          args '-v $HOME/jenkins:/app -p 8000:8000'
        }

      }
      steps {
        sh '''go version
GOPATH=/app
#mkdir /app/.cache
GOCACHE=/app/.cache
apk add --update git'''
        dir(path: 'cidr_convert_api/go/') {
          sh '''ls
#go get github.com/Pepegasca/goop
go get github.com/gorilla/mux
go get github.com/pkg/errors
go get github.com/stretchr/testify/assert
go mod init doot
go mod tidy
go build api.go convert.go
ls
#go run api.go convert.go'''
          archiveArtifacts 'api api.go convert.go'
          sh './api'
        }

      }
    }

  }
}