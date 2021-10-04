pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository

                // Run Maven on a Unix agent.
                sh "mvn clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file. add
                success {
                    archiveArtifacts 'target/*.war'
                }
            }
        }
          stage('docker build') {
              steps {
                sh '''
                docker build -t multipipeline .
                docker run -itd -p 8081:8080 multipipeline
                '''
            }
         }
    }
}