pipeline {
    agent any
    stages {
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    // Define the SonarQube scanner home directory
                    def scannerHome = tool 'SonarQube'

                    // Execute SonarQube scanner with the specified project key and source directory
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=."
                    }
                }
            }
        }
    }
    post {
        always {
            // Record issues found by SonarQube
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}