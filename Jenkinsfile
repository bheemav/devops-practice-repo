pipeline{
    agent any

       stage("Sonar Quality Check"){
            script {
                    withSonarQubeEnv(credentialsId: 'sonarqube-token') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
    
                    }

                }
                
            }
            
    
}
