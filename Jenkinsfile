pipeline {

  environment {
        registry = "soumyanaveen/k8sj:1.0.0"
        registryCredential = 'dockerhub' 
  }

  agent {
    node {
        label 'k8s'
    }
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
               registryCredential = 'dockerhub'
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
