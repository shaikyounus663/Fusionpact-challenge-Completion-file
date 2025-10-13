pipeline {
  agent any
  environment {
    DOCKER_CREDS = credentials('dockerhub')
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Frontend') {
      steps {
        bat "docker build -t frontend-app:latest ./frontend"
      }
    }
    stage('Build Backend') {
      steps {
        bat "docker build -t backend-app:latest ./backend"
      }
    }
    stage('Test Backend') {
      steps {
        bat "docker run --rm backend-app:latest python -m unittest"
      }
    }
    stage('Push to DockerHub') {
      steps {
        bat '''
          echo %DOCKER_CREDS_PSW% | docker login -u %DOCKER_CREDS_USR% --password-stdin
          docker tag frontend-app:latest %DOCKER_CREDS_USR%/frontend-app:latest
          docker tag backend-app:latest %DOCKER_CREDS_USR%/backend-app:latest
          docker push %DOCKER_CREDS_USR%/frontend-app:latest
          docker push %DOCKER_CREDS_USR%/backend-app:latest
        '''
      }
    }
    stage('Deploy') {
      steps {
        bat './deploy.bat'
      }
    }
  }
}
