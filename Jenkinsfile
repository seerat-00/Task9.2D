pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'http://localhost:9000'  // Replace with your SonarQube server URL
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'
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
            echo 'Build and Test and analysis stages completed.'
        }
        failure {
            echo 'Pipeline failed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
    }
}
}
