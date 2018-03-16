#!groovy
def branchVersion = ""
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
         sh 'mvn clean install'
       }
     }
     stage('Sonar') {
            steps {
                sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar -Dsonar.host.url=http://sonar-devel.local"
            }
        }
    
    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
      steps {
        app = docker.build("dockerpoc/FL5")
      }
    }
    
    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Selenium Approach in future ;-) */
      steps{
        app.inside {
            sh 'echo "Tests passed"'
        }
      }
    }

    stage('Push image') {
      
        }
    

  }
}
