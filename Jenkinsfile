pipeline {
    agent any
    tools {
        nodejs 'nodejs'  // Ensure this matches the NodeJS installation name in Jenkins
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test -- --watchAll=false --passWithNoTests'
            }
        }
    }
}
