#!groovy

pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3.5.0'
        }
      }
      steps {
        sh "git checkout ${env.BRANCH_NAME}"
        sh 'mvn clean install'
      }
    }
  
  }
}
