pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker-hub-cred')
    }
    stages {
        stage('build docker image') {
            steps {
                sh 'docker build -t zabdev/evgen:${BUILD-NUMBER} .'
                sh 'echo ${BUILD-NUMBER}'
            }
        }
        stage('push docker image'){
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u zabdev --password-stdin'
                sh 'docker push zabdev/evgen'
            }
        }
        stage('delete local image') {
            steps {
                sh 'docker rmi zabdev/evgen:${BUILD-NUMBER}'
            }
        }
    }
}
