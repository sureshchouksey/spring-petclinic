#!groovy
  def app
pipeline {

 agent any 
  tools {
    jdk 'jdk8'
    maven 'maven3'
  }
  
  stages {
    
     stage('Checkout'){    
       steps {
        sh "git checkout ${env.BRANCH_NAME}"        
       }
     }
     stage ('Java Build') {
       steps {
         sh 'mvn clean install -DskipTests'
       }
     }
     stage('Sonar') {
            steps {
                sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar -Dsonar.host.url=http://sonar-devel.local"
            }
        }
    
   
    
   stage('Create Docker Image') {
  steps{
     sh 'docker build -t Devops-POC5/pipeline:latest .'
   
  }
}


    

  }
}
