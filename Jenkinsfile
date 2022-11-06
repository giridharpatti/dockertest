pipeline {
  agent {
    label 'slavei'
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
        sh 'sudo aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 710222791487.dkr.ecr.ap-south-1.amazonaws.com'
        sh 'sudo docker tag httpd:latest 710222791487.dkr.ecr.ap-south-1.amazonaws.com/demo:${BUILD_NUMBER}'
        sh 'sudo docker push 710222791487.dkr.ecr.ap-south-1.amazonaws.com/demo:${BUILD_NUMBER}'
        }
      }
    }
  }
}
