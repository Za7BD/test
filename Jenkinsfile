pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker-hub-cred')
    }
    stages {
        stage('build docker image') {
            steps {
                sh 'docker build -t zabdev/evgen .'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u zabdev'
                sh 'docker push zabdev/evgen'
            }
        }
    }
}
