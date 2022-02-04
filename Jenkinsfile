pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker-hub-cred')
        REGISTRY = "zabdev/evgen" 
    }
    def app
    stages {
        stage('build docker image') {
            steps {
                script { 
                    dockerImage = docker.build REGISTRY + ":$BUILD_NUMBER" 
                }
            }
        }
        stage(push image){
            steps {
            script { 
                    docker.withRegistry( '', DOCKERHUB_CREDENTIALS ) { 
                        dockerImage.push() 
                    }
                }                 
              } 
            }
        }
    }
}
