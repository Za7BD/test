pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker-hub-cred')
    }
    stages {
        stage('build docker image') {
            steps {
                sh 'docker build -t zabdev/evgen:${BUILD_NUMBER}.0 .'
                sh 'echo ${BUILD_NUMBER}'
            }
        }
        stage('push docker image'){
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u zabdev --password-stdin'
                sh 'docker push zabdev/evgen:${BUILD_NUMBER}.0'
            }
        }
        stage('delete local image') {
            steps {
                sh 'docker rmi zabdev/evgen:${BUILD_NUMBER}.0'
            }
        }
        stage (deploy to cluster){
            steps {
                sh 'echo deploy'
            }
        }
    }
}
