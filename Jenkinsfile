pipeline {
  agent any
  stages {
    stage('Build') {
      agent {
        docker {
          args '-v $HOME/jenkins:/app'
          image 'jynleazy/go-dott:10'
        }

      }
      steps {
        sh '''go version
GOPATH=/app
mkdir -p /app/.cache
GOCACHE=/app/.cache
'''
        dir(path: 'cidr_convert_api/go/') {
          catchError(message: 'failed unit tests', catchInterruptions: true, buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
            sh '''go get github.com/t-yuki/gocover-cobertura
pwd
ls
go test -coverprofile=coverage.out 2>/dev/null
#set +e


'''
          }

          catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
            sh '''gocover-cobertura < coverage.out > coverage.xml
head coverage.xml'''
          }

          catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
            sh 'go test'
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

    stage('Run in a docker container') {
      agent {
        docker {
          args '-p 8000:8000 -p 8001:8001 -p 8002:8002 -v /opt/dott:/app'
          image 'jynleazy/go-dott:12'
        }

      }
      steps {
        sh '''ls
go version
pwd
#./api
ls /app'''
      }
    }

  }
  environment {
    SONARKEY = credentials('tokensonar')
    SONARHOST = 'http://52.4.174.27:9000/'
  }
}