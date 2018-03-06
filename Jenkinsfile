node {
    stage 'checkout' {
    git 'https://github.com/dhirajg27/spring-petclinic.git' 
    
    // checkout input branch 
 steps {
    sh "git checkout ${env.BRANCH_NAME}"
}
}
    stage 'build' {
   steps {
        sh 'mvn clean install'
      }
}
    
    
}
