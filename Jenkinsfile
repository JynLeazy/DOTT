pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          image 'golang:alpine3.13'
          args '-v $HOME/jenkins:/app'
        }

      }
      steps {
        sh '''go version
GOPATH=/app
#mkdir /app/.cache
GOCACHE=/app/.cache
apk add --update git'''
        dir(path: 'cidr_convert_api/go/') {
          sh '''go get github.com/gorilla/mux
go get github.com/pkg/errors
go get github.com/stretchr/testify/assert
cd ../.. && go mod init
go install
'''
        }

      }
    }

  }
}