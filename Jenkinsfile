#!groovy

pipeline {
  def branchVersion = ""
  agent {       label 'puppet'     }
  tools {
    jdk 'jdk8'
    maven 'maven3'
  }
  
  stages {
     stage('Checkout'){    
       steps {
        sh "git checkout ${env.BRANCH_NAME}"
        sh 'mvn clean install'
       }
     }
     stage ('Java Build') {
       steps {
         sh 'mvn clean package -U'
       }
     }
  }
}
