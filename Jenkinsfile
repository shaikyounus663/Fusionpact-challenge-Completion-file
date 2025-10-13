pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        bat 'docker build -t app:latest .'
      }
    }
    stage('Test') {
      steps {
        bat 'docker run --rm app:latest npm test'
      }
    }
    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'younus49', passwordVariable: 'dckr_pat_EfG-UYTTEy3JzFLWlqFkchlLHWU')]) {
          bat 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
          bat 'docker tag app:latest $DOCKER_USER/app:latest'
          bat 'docker push $DOCKER_USER/app:latest'
        }
      }
    }
    stage('Deploy') {
      steps {
        // Use your deployment commands or script here
        bat './deploy.bat'
      }
    }
  }
}
