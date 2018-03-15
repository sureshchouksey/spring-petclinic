#!groovy
def branchVersion = ""
pipeline {
  agent none
      tools {
        jdk 'jdk8'
        maven 'maven3'
    }
  stages {
     stage('Checkout'){

           // checkout repository
          checkout scm
        steps {
        sh "git checkout ${env.BRANCH_NAME}"
        }
       
    }
     stage ('Java Build') {
    // build .war package
       steps {
         sh 'mvn clean package -U'
       }
  }
  }
}
