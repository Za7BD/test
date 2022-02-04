kpipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker-hub-cred')
    }
    def app
    stages {
        stage('build docker image') {
            steps {
                app = docker.build("zabdev/evgen")  
            }
        }
        stage('push image'){
            steps {
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-cred') {            
                app.push("${env.BUILD_NUMBER}")                 
              } 
            }
        }
    }
}

