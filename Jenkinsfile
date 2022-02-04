pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker-hub-cred')
        REGISTRY = "zabdev/evgen" 
    }
    stages {
        stage('build docker image') {
            steps {
                script { 
                    dockerImage = docker.build REGISTRY + ":$BUILD_NUMBER" 
                }
            }
        }
        }
    }
