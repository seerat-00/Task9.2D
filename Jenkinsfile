pipeline {
    agent any
    tools {
        nodejs 'nodejs'  // Ensure NodeJS is installed
    }
    environment {
        SONARQUBE_SERVER = 'http://localhost:9000'  // Replace with your SonarQube server URL
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/seerat-00/Task9.2D.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Build') {
            steps {
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
