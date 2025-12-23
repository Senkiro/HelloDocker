pipeline {
  agent any

  environment {
    IMAGE = "hello_docker"
    CONTAINER = "hello_docker"
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build image') {
      steps {
        sh """
          docker build -t ${IMAGE}:${BUILD_NUMBER} -t ${IMAGE}:latest .
        """
      }
    }

    stage('Deploy local') {
      steps {
        sh """
          docker stop ${CONTAINER} || true
          docker rm ${CONTAINER} || true

          docker run -d --restart unless-stopped --name ${CONTAINER} ${IMAGE}:latest

          docker ps --filter "name=${CONTAINER}"
        """
      }
    }
  }
}
