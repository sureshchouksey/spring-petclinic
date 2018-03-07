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
        checkout scm
	sh 'git checkout branch-poc' 
        sh 'mvn clean install'
      }
    }
    
  }
}
