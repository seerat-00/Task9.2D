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
    }
    post {
        always {
            echo 'Build stage completed.'
        }
        failure {
            echo 'Build failed.'
        }
        success {
            echo 'Build succeeded!'
        }
    }
}
