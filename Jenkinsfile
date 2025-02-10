pipeline {
  agent any
  environment {
    DOCKER_HUB_CREDENTIALS = credentials('158ce399-beca-43ca-85cc-1483d9e1b9b0')
  }
  stages {
    stage('Clone Repository') {
      steps {
        git branch: 'master', url: 'https://github.com/ravijadhav249/todo-app.git'
      }
    }
    stage('Build with Maven') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }
    stage('Build and Push Docker Image') {
      steps {
        sh 'docker build -t ravijadhav249/todo-application:latest .'
        sh 'echo $DOCKER_HUB_CREDENTIALS_PSW | docker login -u $DOCKER_HUB_CREDENTIALS_USR --password-stdin'
        sh 'docker push ravijadhav249/todo-application:latest'
      }
    }
    stage('Deploy with Docker Compose') {
      steps {
        sh 'docker compose-up -d'
      }
    }
    stage('Clean Workspace') {
      steps {
        sh 'rm -rf *'
      }
    }
  }
}
