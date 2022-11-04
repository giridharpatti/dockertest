pipeline {
  agent {
    label 'slave1'
  }
  environment{
     CODEDIR='/var/lib/jenkins/workspace/docker-build/dockertest'    
    }
  stages {
     stage('clone repo') {
       steps {
        sh "rm -rf *"
        sh "git clone -b develop git@bitbucket.org:anuraggoyallh26/web-front.git"
       }
     }
    stage('Build') {
      steps {
        dir("${env.CODEDIR}") {
        echo 'Building docker-compose'
        sh 'docker-compose build'
        }
      }
    }
    stage('Deploy') {
      steps {
        dir("${env.CODEDIR}") {
        echo 'Up the docker container'
        sh 'docker-compose up -d'
        }
      }
    }
  }
}
