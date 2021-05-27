Ansible Roles


  For install roles i found this page
  #the awesome geerling's roles are mentioned in this page
  https://www.scaleway.com/en/docs/how-to-configure-ansible-galaxy/

  Jenkins Role
  
  
      # This was the first role I found
      https://galaxy.ansible.com/jackl0phty/ansible-role-jenkins
      and this his github repo
      https://github.com/jackl0phty/ansible-role-jenkins
      but this repo is a fork from this awesome guy repo
      https://github.com/geerlingguy/ansible-role-jenkins
      and this is my finally Role
     --- geerlingguy.jenkins ---
      We also need a java role for install Jenkins, and Geerling also has one
      --- geerlingguy.java ---
  
  Docker Role
  
  
      #The awesome guy, Jeff Geerling, also have a Docker role
      https://github.com/geerlingguy/ansible-role-docker
      this is the role
      --- geerlingguy.docker ---
      Hi also has this book
      # https://www.ansiblefordevops.com/
      
  SonarQube Role
  
  
  
      #Unfourtanly i didnt found a Geerling repo for this role
      but i found this 2, but I'll try both, before decide which use
      https://github.com/lrk/ansible-role-sonarqube
      https://github.com/lean-delivery/ansible-role-sonarqube
      also i found this web about ansible sonarqube role 
      https://medium.com/@mattpwest/setting-up-sonarqube-with-ansible-fcabadee6953
      and i also found
      https://aws.amazon.com/premiumsupport/knowledge-center/ec2-enable-epel/
      that amazon linux need yo enable epel (Extra Packages for Enterprise Linux), to install it
      
      After several tries, i move to docker container 
      https://hub.docker.com/_/sonarqube?tab=description
      https://docs.sonarqube.org/latest/setup/get-started-2-minutes/
      
      i used this command
      
      docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest
      
      some documentation for sonarqube
      https://docs.sonarqube.org/latest/setup/install-server/
      https://www.youtube.com/watch?v=pufcNkJPvxw
      
      jenkins pluggin for sonarscanner
      https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-jenkins/
      
      exec commands inside docker container
      https://www.edureka.co/community/10588/how-can-i-run-a-docker-exec-command-inside-a-docker-container
      
      github token for jenkins
      https://github.com/settings/tokens/new?scopes=repo,read:user,user:email,write:repo_hook


GO
    
 Go tutorial
 
 https://golang.org/doc/tutorial/greetings-multiple-people   
    
 how install golang
 https://golang.org/doc/install
    
how install a packege with go

https://stackoverflow.com/questions/30295146/how-can-i-install-a-package-with-go-
https://golang.org/cmd/go/

go modules
https://blog.golang.org/using-go-modules
https://golang.org/doc/tutorial/create-module
https://golang.org/doc/modules/developing
https://stackoverflow.com/questions/67306638/go-test-results-in-go-cannot-find-main-module-but-found-git-config-in-users
https://stackoverflow.com/questions/57591085/behaviour-of-go-mod-tidy-vs-go-build


Wh* does go?

https://stackoverflow.com/questions/50633092/where-does-go-get-install-packages
https://stackoverflow.com/questions/30612611/what-does-go-build-build-go-build-vs-go-install


how change cache do dir
https://stackoverflow.com/questions/48983303/how-to-change-cache-directory-during-the-go-build-process


go test

https://golang.org/doc/tutorial/add-a-test
https://levelup.gitconnected.com/automating-build-and-test-of-go-application-with-jenkins-9f96879b5479
https://medium.com/rungo/unit-testing-made-easy-in-go-25077669318

golint

https://www.perforce.com/blog/qac/what-lint-code-and-why-linting-important
https://github.com/golang/lint
http://networkbit.ch/golang-golint/

go coverage
https://blog.golang.org/cover#:~:text=Test%20coverage%20is%20a%20term,the%20test%20coverage%20is%2080%25.&text=An%20early%20test%20coverage%20tool%20for%20Go%20even%20worked%20the%20same%20way.
https://stackoverflow.com/questions/24627871/how-to-maintain-good-go-package-test-coverage-when-dealing-with-obscure-errors
https://stackoverflow.com/questions/10516662/how-to-measure-test-coverage-in-go
https://docs.sonarqube.org/latest/analysis/coverage/

go artifacts

https://docs.gocd.org/current/configuration/managing_artifacts_and_reports.html
  
Reading the DOCKERFILE (DF)


This is how FROM works https://docs.docker.com/engine/reference/builder/#from
The DF, take the golang:1.10-alpine image and installed, that image can be replaced with the newest golang:alpine3.13
This is how ENV works https://docs.docker.com/engine/reference/builder/#env
the DF will create the enviroment funtion GOPATH and give it the path "/go:/app"
This is how RUN works https://docs.docker.com/engine/reference/builder/#run
The DF will install git
This is how WORKDIR works https://docs.docker.com/engine/reference/builder/#workdir
The DF will create and move to the directory "/app"
This is how COPY works https://docs.docker.com/engine/reference/builder/#copy
The DF will copy goopfile from (my repo) "/go" and copy to the docker "/app"
The next RUN, install goop from the repo give it (github.com/Pepegasca/goop)
The next COPY, will copy all "/go/" directory




Jenkins

Allow jenkins run docker
https://docs.docker.com/engine/install/linux-postinstall/
https://stackoverflow.com/questions/39638772/make-jenkins-run-docker-without-sudo


SSH aws connection  error :|

https://aws.amazon.com/premiumsupport/knowledge-center/ec2-linux-resolve-ssh-connection-errors/


Jenkinsfile

blueocean pipeline
https://www.jenkins.io/doc/book/blueocean/pipeline-editor/
https://www.jenkins.io/doc/book/blueocean/pipeline-run-details/
https://medium.com/ecs-digital/building-a-ci-pipeline-with-blue-ocean-6bb9b02788eb

Jenkins pipeline how to change to another folder
https://stackoverflow.com/questions/52372589/jenkins-pipeline-how-to-change-to-another-folder


Run Jenkins as a root, in case jenkins don´t have persmissions to create directorys

https://stackoverflow.com/questions/29926773/run-shell-command-in-jenkins-as-root-user
https://stackoverflow.com/questions/50646845/getting-sudo-unknown-uid-xxx-who-are-you-in-jenkins-pipeline-thats-building
https://docs.docker.com/engine/install/linux-postinstall/

jenkins error exit code 1

https://stackoverflow.com/questions/60943751/how-to-fix-script-returned-exit-code-1-when-running-jenkins-pipeline


How to build on Jenkins and publish artifacts via ssh with Pipelines

https://medium.com/@weblab_tech/how-to-publish-artifacts-in-jenkins-f021b17fde71


Jenkins Pipeline with Sonarqube and Gitlab

https://medium.com/appfleet/jenkins-pipeline-with-sonarqube-and-gitlab-ebcca5ef2ebd#:~:text=Go%20Dashboard%20%3E%20Manage%20Jenkins%20%3E%20Manage,the%20result%20to%20SonarQube%20Server.


Handling Environment Variables 
https://www.jenkins.io/doc/book/security/environment-variables/

jenkins junit plugin -already install
https://plugins.jenkins.io/junit/

move foward stage jenkins
https://stackoverflow.com/questions/40600621/continue-jenkins-pipeline-past-failed-stage
https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/

jenkins credentials
https://www.jenkins.io/doc/book/using/using-credentials/

jenkins env vars
https://www.jenkins.io/doc/pipeline/tour/environment/

jenkins  handling credentials in env vars
https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#handling-credentials


jenkins test artifacts
https://www.jenkins.io/doc/pipeline/tour/tests-and-artifacts/

Alpine

https://wiki.alpinelinux.org/wiki/GCC
https://stackoverflow.com/questions/50984864/installing-gcc-from-source-on-alpine
https://wiki.alpinelinux.org/wiki/Alpine_Linux_package_management

GCC (the GNU Compiler Collection)

https://stackoverflow.com/questions/43580131/exec-gcc-executable-file-not-found-in-path-when-trying-go-build


SonarQube

https://docs.sonarqube.org/latest/requirements/requirements/
https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/
https://docs.sonarqube.org/latest/analysis/analysis-parameters/

sonnarqube coverage
https://community.sonarsource.com/t/sonargo-code-coverage-0/19473/9

sonar scanner
https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/

sonar login error
https://community.sonarsource.com/t/not-authorized-please-check-the-properties-sonar-login-and-sonar-password/17452

set up sonarqube in docker container 
https://medium.com/@HoussemDellai/setup-sonarqube-in-a-docker-container-3c3908b624df

sonar-scanner for jenkins
https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-jenkins/

sonar token
https://docs.sonarqube.org/latest/user-guide/user-token/

sonar-scanner docker
https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/

sonarsource for go
https://www.sonarsource.com/go/
https://docs.sonarqube.org/latest/analysis/languages/go/


Docker

docker run flags
https://docs.docker.com/engine/reference/run/
https://linuxize.com/post/docker-run-command/

docker open ports
https://docs.docker.com/config/containers/container-networking/

change dir inside docker
https://stackoverflow.com/questions/44637748/change-directory-in-docker-alpine-failing
https://stackoverflow.com/questions/49683612/copy-current-directory-in-to-docker-image

build docker image
https://docs.docker.com/get-started/02_our_app/

docker stops automatically after run cmd
https://stackoverflow.com/questions/30209776/docker-container-will-automatically-stop-after-docker-run-d

docker change dir alpine
https://stackoverflow.com/questions/44637748/change-directory-in-docker-alpine-failing

Linux
standar error
https://www.cyberciti.biz/faq/unix-linux-redirect-error-output-to-null-command/

entr cmd
http://eradman.com/entrproject/

lib elf interpreter
https://support.quest.com/es-es/kb/117266/-lib-ld-linux-so-2-bad-elf-interpreter-no-such-file-or-directory

docker images

sonar-scanner
https://hub.docker.com/r/sonarsource/sonar-scanner-cli/tags?page=1&ordering=last_updated


https://golang.org/doc/tutorial/compile-install
https://ieftimov.com/post/testing-in-go-go-test/
https://www.whitesourcesoftware.com/free-developer-tools/blog/golang-dependency-management/
https://golang.org/doc/tutorial/getting-started
https://stackoverflow.com/questions/37710108/go-coverage-report-integration-with-jenkins
https://docs.sonarqube.org/latest/requirements/requirements/
https://hub.docker.com/_/golang?tab=tags&page=2&ordering=last_updated







