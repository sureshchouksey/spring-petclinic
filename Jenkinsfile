#!groovy

node {
  agent none
  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3.5.0'
        }
      }
    	
      steps ('Checkout') {
        git 'https://github.com/dhirajg27/spring-petclinic.git' 
	sh 'git checkout "${env.BRANCH_NAME}"' 
        sh 'mvn clean install'
      }
    }
    
  }
}
