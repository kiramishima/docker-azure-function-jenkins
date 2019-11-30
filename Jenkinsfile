pipeline {
  agent any

  options {
    disableConcurrentBuilds()
  }

  stages {
    stage('Build') {
      steps {
        echo 'Building Docker Image'
        buildApp()
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh 'echo "Deploying"'
            deploy('dev')
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

def buildApp() {
  def appImage = docker.build("kiramishima/azf_jenkins:${BUILD_NUMBER}")
}

def deploy(environment) {

	def containerName = ''
	def port = ''

	if ("${environment}" == 'dev') {
		containerName = "app_dev"
		port = "8888"
	}
	else {
		println "Environment not valid"
		System.exit(0)
	}

	sh "docker ps -f name=${containerName} -q | xargs --no-run-if-empty docker stop"
	sh "docker ps -a -f name=${containerName} -q | xargs -r docker rm"
	sh "docker run -d -p ${port}:80 --name ${containerName} kiramishima/azf_jenkins:${BUILD_NUMBER}"

}