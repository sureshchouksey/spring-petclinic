#!groovy

pipeline {
  agent none
      tools {
        jdk 'jdk8'
        maven 'maven3'
    }
  def branchVersion = ""
  stages {
     stage('Checkout'){          
     steps {
        sh "git checkout ${env.BRANCH_NAME}"
        sh 'mvn clean install'
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
