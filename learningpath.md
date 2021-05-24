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
      
      
 GO
    

  
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









https://golang.org/doc/tutorial/compile-install
https://ieftimov.com/post/testing-in-go-go-test/
https://www.whitesourcesoftware.com/free-developer-tools/blog/golang-dependency-management/
https://golang.org/doc/tutorial/getting-started
https://stackoverflow.com/questions/37710108/go-coverage-report-integration-with-jenkins
https://docs.sonarqube.org/latest/requirements/requirements/
https://hub.docker.com/_/golang?tab=tags&page=2&ordering=last_updated
