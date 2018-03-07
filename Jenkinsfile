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
     stage('Results - 1') {
         junit '**/target/surefire-reports/TEST-*.xml'
         archive 'target/*.jar'
    }
    
    stage 'bake image'
    docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials') {
        def image = docker.build("ravisankar/ravisankardevops:${env.BUILD_TAG}",'.')
        
        stage 'test image'
        image.withRun('-p 8888:8888') {springboot ->
        sh 'while ! httping -qc1 http://localhost:8888/info; do sleep 1; done'
        git 'https://github.com/RavisankarCts/petclinicacceptance.git'
        sh 'mvn clean verify'
        }
        
        stage('Results') {
         junit '**/target/surefire-reports/TEST-*.xml'
         archive 'target/*.jar'
        }
        
        stage 'push image'
        image.push()
    }
  
  }
}
