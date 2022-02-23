pipeline {

  environment {
    myEnv=""
    script {
     if (env.BRANCH_NAME == 'master') {
       myEnv='production'
      } else {
       myEnv='staging'
      }
    }
    dockerimagename = "zabdev/evgen:${env.BUILD_ID}.0"
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
            dockerImage.push("${env.BUILD_ID}.0")
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
          kubernetesDeploy(configs: "k8s_deploy.yml", kubeconfigId: "kubernetes-id")
        }
      }
    }
  }
}

