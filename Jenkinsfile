pipeline {

  environment {
        registry = "dockerqprofiles/j2k"
        registryCredential = 'DockerHubCreds' 
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git branch: 'main', url: 'https://github.com/gitqprofiles/J2K.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + "latest"
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'DockerHubCreds'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}
