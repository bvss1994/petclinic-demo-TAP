pipeline {
  environment {
    registry = "sowmyabv123/petclinic"
    registryCredential = 'docker_hub'
    dockerImage = ''
  }
  agent any
  stages{
    stage ('Build') {
      steps{
        echo "Building Project"
        sh './mvnw package'
      }
    }
    stage ('Archive') {
      steps{
        echo "Archiving Project"
        archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
      }
    }
    stage ('Build Docker Image') {
      steps{
        echo "Building Docker Image"
         script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage ('Push Docker Image') {
      steps{
        echo "Pushing Docker Image"
         script {
          docker.withDockerRegistry('', registryCredential) {
              dockerImage.push()
          }
        }
      }
    }
    stage ('Deploy to Dev') {
      steps{
        echo "Deploying to Dev Environment"
      }
    }
  }
}
