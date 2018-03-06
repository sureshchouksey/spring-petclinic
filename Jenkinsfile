node {
    stage 'checkout'
    git 'https://github.com/dhirajg27/spring-petclinic.git' 
    
    // checkout input branch 
    sh "git checkout ${env.BRANCH_NAME}"
    stage 'build'
    sh 'mvn clean install'
    
    
}
