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
        sh '''
        docker-compose build &&
        sudo docker tag dockertest-web:latest 710222791487.dkr.ecr.ap-south-1.amazonaws.com/demo:${BUILD_NUMBER} &&
        sudo aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 710222791487.dkr.ecr.ap-south-1.amazonaws.com &&
        sudo docker push 710222791487.dkr.ecr.ap-south-1.amazonaws.com/demo:${BUILD_NUMBER}
        '''
        }
      }
    }
  }
}
