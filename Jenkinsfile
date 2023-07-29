pipeline {
  environment {
    imagename = "venkatbramhasani/free-css-templates"
    registryCredential = 'dockerhub-credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/VenkatBramhasani/Kubernetes_Project.git', branch: 'main', credentialsId: 'VenkatBramhasani'])
 
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
          echo "Build image succeeded"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          echo "Deploy image processed"
          docker.withRegistry( '', registryCredential ) {
          dockerImage.push('dockerImage')
          dockerImage.push('latest')
					}
          echo "Deploy image succeeded"
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"
 
      }
    }
  }
}
