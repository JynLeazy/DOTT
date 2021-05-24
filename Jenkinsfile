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
        sh '''pwd
ls'''
      }
    }

  }
}