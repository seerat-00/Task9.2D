pipeline {
    agent any
    environment {
        SONARQUBE_SERVER = 'http://localhost:9000'
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'
                bat 'npm install crypto-browserify'
                bat 'set CI=false && npm run build'
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
