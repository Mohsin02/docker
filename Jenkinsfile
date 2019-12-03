pipeline {
  environment {
    registry = "mohsindocker/dockerapp"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
         // dockerImage = docker.build registry + ":$BUILD_NUMBER"
    
         dockerImage = docker.build("mohsindocker/dockerapp")
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( credentialsId: 'dockerRegistryCredentials', url: 'mohsindocker' ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}