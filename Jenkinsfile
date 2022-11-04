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
        sh "git clone -b develop git@github.com:giridharpatti/dockertest.git"
       }
     }
    stage('Build') {
      steps {
        dir("${env.CODEDIR}") {
        echo 'Building docker-compose'
        sh 'sudo docker-compose build'
        }
      }
    }
    stage('Deploy') {
      steps {
        dir("${env.CODEDIR}") {
        echo 'Up the docker container'
        sh 'sudo docker-compose up -d'
        }
      }
    }
  }
}
