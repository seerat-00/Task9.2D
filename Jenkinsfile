pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building the project...'
        sh 'npm install'
        sh 'npm audit'
      }
    }
  }
  post {
    success {
      echo 'Build succeeded!'
    }
    failure {
      echo 'Build failed!'
    }
  }
}
