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
          
          // save our docker build context before we switch branches
          sh "cp -r ./.docker/build tmp-docker-build-context"
         
          sh "git checkout ${env.BRANCH_NAME}"     
          
       }
     }
     stage ('Java Build') {
       steps {
         //sh 'mvn clean install -DskipTests'
         sh 'mvn clean package -U'
       }
     }
     stage('Sonar') {
            steps {
                sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar -Dsonar.host.url=http://sonar-devel.local"
            }
        }
    
   
    
   stage('Create Docker Image') {
     steps{
       // prepare docker build context
      //sh "cp /target/spring-petclinic-2.0.0.BUILD-SNAPSHOT.jar ./tmp-docker-build-context"
      sh 'docker build -t Devops-POC5/pipeline:latest .'
   
  }
}


    

  }
}
