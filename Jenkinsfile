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
cd cidr_convert_api/go/'''
        dir(path: 'cidr_convert_api/go/') {
          sh '''whoami
ls -lah /
#go get github.com/gorilla/mux
#go get github.com/pkg/errors
#go get github.com/stretchr/testify/assert'''
        }

      }
    }

  }
}