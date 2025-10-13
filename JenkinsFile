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
        sh 'docker build -t app:latest .'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run --rm app:latest npm test'
      }
    }
    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'younus49', passwordVariable: 'dckr_pat_EfG-UYTTEy3JzFLWlqFkchlLHWU')]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
          sh 'docker tag app:latest $DOCKER_USER/app:latest'
          sh 'docker push $DOCKER_USER/app:latest'
        }
      }
    }
    stage('Deploy') {
      steps {
        // Use your deployment commands or script here
        sh './deploy.sh'
      }
    }
  }
}
