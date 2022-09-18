pipeline{
    agent any 
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages{
        stage("sonar quality check"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonartoken') {
                            sh 'chmod +x gradlew'
                            sh './gradlew SonarQube'
                            sh  'java -version'
                    }
                    timeout(time: 3, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status = 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }  
                }
            }
        }
    }
}

                
