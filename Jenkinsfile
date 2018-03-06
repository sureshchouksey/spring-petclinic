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
        git 'https://github.com/dhirajg27/spring-petclinic.git' 
	sh "git checkout ${env.BRANCH_NAME}"
      }
      steps {
        sh 'mvn clean install'
      }
    }
    
  }
}
