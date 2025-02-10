pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the React project...'
                bat '''
                    npm install
                    npm run build
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'npm test -- --watchAll=false --passWithNoTests'
            }
        }
        stage('Code Quality Analysis') {
            steps {
                echo 'Running SonarQube analysis...'
                withSonarQubeEnv('SonarQube') { // 'SonarQube' should match your Jenkins configuration name
                    bat '''
                        sonar-scanner.bat ^
                        -Dsonar.projectKey=task9.2c ^
                        -Dsonar.sources=./src ^
                        -Dsonar.host.url=http://localhost:9000 ^
                        -Dsonar.login=sqa_6dc4d38c5c2032383b2f88675e479eaee84c9f47
                    '''
                }
            }
        }
    }
    post {
        always {
            echo 'Build, Test, and Code Quality Analysis stages completed.'
        }
        failure {
            echo 'Pipeline failed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
    }
}
