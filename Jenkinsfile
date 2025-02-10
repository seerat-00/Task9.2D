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
                archiveArtifacts artifacts: 'build/**', fingerprint: true
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
