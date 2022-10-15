pipeline{
    agent any

    stages{
        stage("Sonar Quality Check"){
            agent{
                docker{
                    image 'openjdk:8-jdk-alpine'
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
