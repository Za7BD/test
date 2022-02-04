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
        stage ('deploy to cluster'){
            steps {
                sh 'echo "apiVersion: apps/v1
kind: Deployment
metadata:
  name: evgen-deployment
  labels:
    app: evgen-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: evgen-app
  template:
    metadata:
      labels:
        app: evgen-app
    spec:
      containers:
      - name: evgen-app-cont
        image: zabdev/evgen:${BUILD_NUMBER}.0
        ports:
        - containerPort: 80"
 > deploy.yml'
            }
        }
    }
}
