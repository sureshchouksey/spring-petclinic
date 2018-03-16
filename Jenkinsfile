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
                sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3:sonar -Dsonar.host.url=http://sonar-devel.local"
            }
        }
  }
}
