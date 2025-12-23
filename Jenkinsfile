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
          docker rm -f hello_docker || true
          docker run --rm --name hello_docker hello_docker:latest
        '''
      }
    }
  }
}
