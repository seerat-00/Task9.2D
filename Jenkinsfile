pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'http://localhost:9000'  // Replace with your SonarQube server URL
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'
                // Add a step to install crypto-browserify if needed
                bat 'npm install crypto-browserify'
                bat 'npm run build'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test -- --watchAll=false --passWithNoTests'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarScanner') {
                    bat '''
                        npx sonar-scanner ^
                        -Dsonar.projectKey=jenkins-demo ^
                        -Dsonar.sources=src ^
                        -Dsonar.host.url=%SONARQUBE_SERVER%
                    '''
                }
            }
        }
    }
    post {
        always {
            echo 'Build, Test, and SonarQube Analysis stages completed.'
        }
        failure {
            echo 'Pipeline failed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
    }
}
