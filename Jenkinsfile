pipeline {
  environment {
    imagename = "venkatbramhasani/free-css-templates"
    registryCredential = 'dokcer-hub-venkatbramhasani'
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
          dockerImage = 'docker.build(imagename + ":$BUILD_NUMBER")'
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
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
