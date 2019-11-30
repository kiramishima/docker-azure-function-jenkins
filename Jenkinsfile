pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building Docker Image'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh 'echo "Deploying"'
          }
        }

        stage('Testing Deploy') {
          steps {
            echo 'Funciona bien'
          }
        }

      }
    }

  }
}