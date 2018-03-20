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
         //sh 'mvn clean install -DskipTests'
         sh 'mvn clean package -U'
       }
     }
     stage('Sonar') {
            steps {
               sh "whoami"
               // sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar -Dsonar.host.url=http://sonar-devel.local"
            }
        }
    
   
    
   stage('Create Docker Image') {
     steps{
       //sh "pwd"
       // prepare docker build context
      //sh "cp /target/spring-petclinic-2.0.0.BUILD-SNAPSHOT.jar ./tmp-docker-build-context"
      sh "sudo docker ps -a" 
      sh "sudo docker build -t devops-poc/pipeline:latest ."
   
  }
}
 stage('Run Docker Image') {
     steps{
         sh "docker run -p8082:8080  devops-poc/pipeline:latest"        
  }
}


    

  }
}
