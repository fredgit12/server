pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerHublogin')
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "My first pipeline"'
                sh '''
                    echo "By the way, I can do more stuff in here"
                    ls -lah
                    sh 'docker build -t karl2022/server:latest .'
                '''
            }
        }
        stage('Publish') {
            steps {
                sh '''
                    docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
                    docker push karl2022/server:latest
                    docker logout
                   '''
      }
    }
  }
}
