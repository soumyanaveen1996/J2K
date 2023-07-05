pipeline {

  environment {
        registry = "soumyanaveen"
        registryCredential = 'dockerhub' 
  }

 

  stages {

    stage('Checkout Source') {
      steps {
        git branch: 'main', url: 'https://github.com/soumyanaveen1996/J2K.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'docker'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

  

  }
}
