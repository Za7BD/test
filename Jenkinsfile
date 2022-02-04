pipeline {
    agent any

    stages {
        stage('build docker image') {
            steps {
                sh 'docker build -t zabdev/evgen .'
                sh 'docker push zabdev/evgen'
            }
        }
    }
}

