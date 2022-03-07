pipeline {

  environment {
    dockerimagename = "karl2022/server"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/fredgit12/server.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerHublogin'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
      stage('Deploy') {
            steps{
        script {
          kubernetesDeploy(configs: "nodejsapp.yaml", kubeconfigId: "kuberID") {
          }
        }
      }
    }
  }    
}
}  
