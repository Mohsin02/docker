pipeline {
  environment {
    registry = "mohsindocker/dockerapp"
    registryCredential = 'dockerhub'
    dockerImage = ''
    DOCKER_TAG = getDockerTag()
  }
  agent any
  stages {
   stage('Building image') {
      steps{
       
      
      docker.build("test-image", "Dockerfile")
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

def getDockerTag(){
    
 def tag = sh script: 'git rev-parse HEAD', returnStdout: true
 return tag
}

