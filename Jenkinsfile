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
        // checkout input branch 
        sh "git checkout ${env.BRANCH_NAME}"
       
    }
     stage ('Java Build') {
    // build .war package
    sh 'mvn clean package -U'
  }
  }
}
