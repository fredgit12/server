pipeline{
    agent any
    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerHublogin')
    stages {
        
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t karl2022/server:latest .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                    
                 
                    sh 'docker login -u karl2022 -p ${DOCKERHUB_CREDENTIALS}'
                 
                    sh 'docker push karl2022/server:latest'
                }
            }
        }
    
    stage('Deploy App on k8s') {
      steps {
            sshagent(['']) {
                sh "scp -o StrictHostKeyChecking=no nodejsapp.yaml root@194.233.162.114:/home/ubuntu"
            script {
                try{
                    sh "ssh root@194.233.162.114 kubectl create -f ."
                }catch(error){
                    sh "ssh root@194.233.162.114 kubectl create -f ."
                            }   
                }
            }
        }
      
    }
    }
    }
}
