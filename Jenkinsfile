pipeline {
  agent {
    label 'ubuntu'
  }
  environment{
     CODEDIR='/home/ubuntu/jenkins/workspace/nagarro-build/dockertest'    
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
        echo 'Building docker image'
        sh '''
        docker build -t webapp:${BUILD_NUMBER} . &&
        docker save -o webapp_${BUILD_NUMBER}.tar webapp:${BUILD_NUMBER} &&
        aws s3 cp webapp_${BUILD_NUMBER}.tar s3://s3bucketasdockerimagesstorage/webapp_${BUILD_NUMBER}.tar &&
        docker rmi $(docker images -q)
        '''
        }
      }
    }
  }
}
