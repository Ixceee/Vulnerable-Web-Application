pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the specified Git repository and branch
                git branch: 'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
            }
        }
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