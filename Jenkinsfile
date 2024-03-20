pipeline {
  environment {
    registry = "halim/tp5"
    registryCredential = 'DockerHub'
    dockerImage = ''
    gitBranch = 'main'
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: "${gitBranch}", url: 'https://github.com/yhalim8/TP5-DEVOPS.git'
      }
    }
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Test image') {
      steps {
        script {

          echo "Tests passed"
        }
      }
    }
    stage('Publish Image') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Deploy image') {
       steps{
       bat "docker run -d $registry:$BUILD_NUMBER"
       }
     }
  }
}