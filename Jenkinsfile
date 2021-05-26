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
mkdir -p /app/.cache
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
            sh '''go get github.com/t-yuki/gocover-cobertura
pwd
ls
go test -coverprofile=coverage.out 2>/dev/null
gocover-cobertura < coverage.out > coverage.xml
head coverage.xml
go test
#set +e


'''
          }

          sh '''cp ./* /app/
ls /app/
cat /app/coverage.out'''
        }

      }
    }

    stage('SonarQube') {
      agent {
        docker {
          image 'sonarsource/sonar-scanner-cli'
          args '-v $HOME/jenkins:/usr/src -e SONAR_HOST_URL="$SONARHOST" -e SONAR_LOGIN="$SONARKEY"'
        }

      }
      steps {
        sh '''pwd
ls'''
        dir(path: 'cidr_convert_api/go/') {
          sh '''ls /usr/src
cat /usr/src/coverage.out
sonar-scanner -Dsonar.projectKey=dott -Dsonar.sources=. -Dsonar.host.url="$SONAR_HOST_URL" -Dsonar.login="$SONAR_LOGIN" -Dsonar.go.coverage.reportPaths="/usr/src/coverage.out"
'''
        }

      }
    }

    stage('Deploy') {
      steps {
        junit(testResults: '.xml', allowEmptyResults: true)
        sh '''mkdir -p /opt/dott/
ls /opt/dott/
cp -f $HOME/jenkins/* /opt/dott/
ls /opt/dott/'''
      }
    }

  }
  environment {
    SONARKEY = credentials('dottgotoken')
    SONARHOST = 'http://44.234.64.89/'
  }
}
