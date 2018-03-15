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
         sh 'mvn clean package -U'
       }
     }
     stage('Sonar') {
            steps {
                sh "mvn sonar:sonar -Dsonar.host.url=http://sonar-devel.local:29000/"
            }
        }
  }
}
