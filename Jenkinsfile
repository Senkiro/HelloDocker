pipeline {
  agent any

  environment {
    APP_DIR   = "HelloDocker"
    IMAGE     = "hello_docker"
    CONTAINER = "hello_docker"
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build image') {
      steps {
        dir("${APP_DIR}") {
          sh '''
            pwd
            ls -la
            docker build -t ${IMAGE}:${BUILD_NUMBER} -t ${IMAGE}:latest .
          '''
        }
      }
    }

    stage('Deploy local') {
      steps {
        sh '''
          docker stop ${CONTAINER} || true
          docker rm ${CONTAINER} || true
          docker run -d --restart unless-stopped --name ${CONTAINER} ${IMAGE}:latest
          docker ps --filter "name=${CONTAINER}"
        '''
      }
    }
  }
}
