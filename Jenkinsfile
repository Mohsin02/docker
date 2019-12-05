pipeline {
  environment {
    registry = "mohsindocker/dockerapp"
    registryCredential = 'dockerhub'
    dockerImage = ''
    docker = ''
    DOCKER_TAG = getDockerTag()
  }
  agent any
  stages {
   stage('Building image') {
      steps{
       
      
      docker.withServer('tcp://localhost:2375', 'swarm-certs') {
        docker.image('mysql:5').withRun('-p 3306:3306') {
            /* do things */
        }
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

def getDockerTag(){
    
 def tag = sh script: 'git rev-parse HEAD', returnStdout: true
 return tag
}

