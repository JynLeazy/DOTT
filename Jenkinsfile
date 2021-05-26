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
apk add --update git
'''
        dir(path: 'cidr_convert_api/go/') {
          sh '''ls
ls /app
cp ./* /app
ls /app
#go get github.com/Pepegasca/goop
go get github.com/gorilla/mux
go get github.com/pkg/errors
go get github.com/stretchr/testify/assert
go mod init doot
go mod tidy
go build api.go convert.go
ls
#go run api.go convert.go
'''
          archiveArtifacts 'api'
          sh '''apk add build-base
'''
          catchError(message: 'failed unit tests', catchInterruptions: true) {
            sh '''go test
#set +e
go get github.com/t-yuki/gocover-cobertura
go test -coverprofile=cover.out
gocover-cobertura < cover.out > coverage.xml
head coverage.xml
'''
          }

        }

      }
    }

    stage('Test') {
      agent {
        docker {
          image 'sonarsource/sonar-scanner-cli'
          args '-v $HOME/jenkins:/usr/src -e SONAR_HOST_URL="http://35.81.76.94/" -e SONAR_LOGIN="a8fd5149bbd092aabe4af5656283ce9154bf34f2"'
        }

      }
      steps {
        sh '''pwd
ls'''
        dir(path: 'cidr_convert_api/go/') {
          sh '''ls /usr/src

sonar-scanner -Dsonar.projectKey=dott -Dsonar.sources=api.go convert.go convert_test.go -Dsonar.host.url="$SONAR_HOST_URL" -Dsonar.login="$SONAR_LOGIN" -Dsonar.go.coverage.reportPaths=/usr/src/coverage.out
'''
        }

      }
    }

    stage('Deploy') {
      steps {
        junit(testResults: '.xml', allowEmptyResults: true)
      }
    }

  }
}