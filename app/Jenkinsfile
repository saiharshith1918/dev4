pipeline {
  agent any

  environment {
    DOCKER_USER = credentials('docker-user')
    DOCKER_PASS = credentials('docker-pass')
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/saiharshith1918/dev4.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t harshith1918/cicd-demo:latest .'
      }
    }

    stage('Docker Login') {
      steps {
        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
      }
    }

    stage('Push Image') {
      steps {
        sh 'docker push harshith1918/cicd-demo:latest'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
      }
    }
  }
}
