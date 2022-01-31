pipeline {

  environment {
    dockerimagename = "svabh"
    dockerImage = ""
  }

  agent { label 'jdk11-mvn3.8.4' }
     options {
    buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '2'))
     }

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/svabhi/nodeapp_test.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhubcredentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    // stage('Deploying App to Kubernetes') {
    //   steps {
    //     script {
    //       kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
    //     }
    //   }
    // }

  }

}
