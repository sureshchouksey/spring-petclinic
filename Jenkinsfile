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
    script {
      def apitestimage = docker.build('ockerpoc-5/docker-jenkins-pipeline:${env.BUILD_NUMBER}', '--no-cache=true dockerbuild')
    }
  }
}

stage('Test Dockerimage') {
  steps{
    script {
      apitestimage.inside {
        sh 'echo cd testing && ctest'
      }           
    }
  }
}
    
    

  }
}
