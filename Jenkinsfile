#!groovy
  def app
def emailNotifications = 'manish_nair@fulcrumww.com'
def notificationSent    = false

def sendNotification(buildChanged)
{
    if (notificationSent)
    {
        return
    }
    notificationSent = true

    if (currentBuild.currentResult == 'SUCCESS')
    {
        // notify users when the build is back to normal
        mail to: emailNotifications,
            subject: "Build Successful: ${currentBuild.fullDisplayName}",
            body: "The build is successful ${env.BUILD_URL}"
    }
    else if ((currentBuild.currentResult == 'FAILURE') && buildChanged)
    {
        // notify users when the Pipeline first fails
        mail to: emailNotifications,
            subject: "Build failed: ${currentBuild.fullDisplayName}",
            body: "Something went wrong with ${env.BUILD_URL}"
    }
    else if ((currentBuild.currentResult == 'FAILURE'))
    {
        // notify users when they check into a broken build
        mail to: emailNotifications,
            subject: "Build failed : ${currentBuild.fullDisplayName}",
            body: "Something is still wrong with ${env.BUILD_URL}"
    }
}
pipeline {

 agent any 
  tools {
    jdk 'jdk8'
    jdk7 'jdk7'
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
      sh "sudo docker stop devops-poc/pipeline:latest" 
      sh "sudo docker rm devops-poc/pipeline:latest" 
      sh "sudo docker build -t devops-poc/pipeline:latest ."
          }
     }
 
    stage('Run Docker Image') { 
                       
     steps{
      
         //sh "sudo docker run -p8082:8080  devops-poc-${env.VERSION_NUMBER}/pipeline:latest"     
         sh """
                    sudo docker run -d \
                        -p8082:8080 \
                        -v /var/run/docker.sock:/var/run/docker.sock:ro \
                        -e TIMEOUT=30 \
                        devops-poc/pipeline:latest
            """                        
           } 
       
      }
    stage('Run Smoke Tests') {
      steps {
        node('master') {
              build job: 'smoketest'
            }
      }
    }
         

  }
  post {
        changed {
            sendNotification buildChanged:true
        }
        failure {
            sendNotification buildChanged:false
        }
    }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "manish_nair@fulcrumww.com",
                sendToIndividuals: true])
        }
    }
}
