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
        steps {
           // checkout repository
          checkout scm
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
