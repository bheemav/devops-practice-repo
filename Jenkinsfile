pipeline{
    agent any

    stages{
        stage("Sonar Quality Check"){
            agent{
                docker{
                    image 'openjdk:11'
                }
            }
            
            steps{
                sript {
                    withSonarQubeEnv(credentialsId: 'sonarqube-token') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
    
                    }

                }
                }
            }
            
    }
    post{
        always{
            echo "SUCCESS"
        }
        
    }
}
