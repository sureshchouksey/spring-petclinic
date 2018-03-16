#!groovy

pipeline {
  
 agent any 
  tools {
    jdk 'jdk8'
    maven 'maven3'
  }
  
  stages {
    def app
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
                sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar -Dsonar.host.url=http://sonar-devel.local"
            }
        }
    
    stage('Build image') {
        steps {
          app = docker.build("dockerpoc/FL5")
        }
    }
    
    

  }
}
