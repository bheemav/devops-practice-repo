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
	         timeout(time: 15, unit: 'MINUTES') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }

                }
                }
            }
         stage("docker build & docker push"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker-nexus-repo', variable: 'docker_password')]) {
                             sh '''
                                docker build -t 3.80.160.175:8083/springapp:${VERSION} .
                                docker login -u admin -p $docker_password 3.80.160.175:8083
                                docker push 3.80.160.175:8083/springapp:${VERSION}
                                docker rmi 3.80.160.175:8083/springapp:${VERSION}
                            '''
                   }
                    

                }
            }
        }           
    }
    
}
