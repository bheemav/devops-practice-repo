pipeline{
    agent any

    stages{
        stage("Sonar Quality Check"){
            agent{
                docker{
                    image 'cbush06/bamboo-builder'
                }
            }
            
            steps{
                script {
                    withSonarQubeEnv(credentialsId: 'sonarqube-token') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
    
                    }

                }
                }
            }
            
    }
    
}
