#!groovy

node {
  def branchVersion = ""
  agent none
      tools {
        jdk 'jdk8'
        maven 'maven3'
    }
  
  stages {
     stage('Checkout'){         
        sh "git checkout ${env.BRANCH_NAME}"
        sh 'mvn clean install'
     }
     stage ('Java Build') {
            sh 'mvn clean package -U'
     }
  }
}
