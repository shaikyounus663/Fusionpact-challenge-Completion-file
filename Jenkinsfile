pipeline {
  agent any
  environment {
    DOCKER_USER = credentials('younus49')    // DockerHub username stored in Jenkins credentials
    DOCKER_PASS = credentials('7890shaikyou')    // DockerHub password or PAT stored in Jenkins credentials
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build Frontend') {
      steps {
        var 'docker build -t frontend-app:latest ./frontend'
      }
    }
    stage('Build Backend') {
      steps {
        var 'docker build -t backend-app:latest ./backend'
      }
    }
    stage('Test Backend') {
      steps {
        // Assuming backend container has tests and can run with 'npm test' or change according to your backend test command
        var 'docker run --rm backend-app:latest npm test'
      }
    }
    stage('Push to DockerHub') {
      steps {
        var 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
        var 'docker tag frontend-app:latest %DOCKER_USER%/frontend-app:latest'
        var 'docker tag backend-app:latest %DOCKER_USER%/backend-app:latest'
        var 'docker push %DOCKER_USER%/frontend-app:latest'
        var 'docker push %DOCKER_USER%/backend-app:latest'
      }
    }
    stage('Deploy') {
      steps {
        // Use your deployment commands here, e.g.
        var './deploy.bat'
      }
    }
  }
}
