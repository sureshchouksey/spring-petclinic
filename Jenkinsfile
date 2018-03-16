#!groovy
def branchVersion = ""
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
         sh 'mvn clean install'
       }
     }
     stage('Sonar') {
            steps {
                sh "mvn sonar:sonar -Dsonar.host.url=http://localhost:29000"
            }
        }
  }
}
