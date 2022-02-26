pipeline {

  environment {
    dockerimagename = "zabdev/evgen:${env.GIT_COMMIT}"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'docker-hub-cred'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("${env.GIT_COMMIT}")
          }
        }
      }
    }
    stage('remove local Image') {
      steps{
      echo 'docker rmi -f $dockerimagename'
      }
    }
    stage('Deploying App to Kubernetes') {
      steps {
        script {
            if (env.GIT_BRANCH == 'origin/main') {
            def env.myEnv='production'
              }
          else {
            def env.myEnv='staging'
                }
               }
        
        echo "${env.myEnv}"
      }
    }
  }
}

