pipeline {
  agent any

  tools {
    maven 'M3'
  }

  environment {
    DOCKERHUB_PWD = credentials('dockerhub-password')
    IMAGE_NAME = 'hzyxby1996/comp367-q2:1.0'
    PATH = "/usr/local/bin:${env.PATH}"
  }

  stages {
    stage('Check out') {
      steps {
        git branch: 'main', url: 'https://github.com/evelynhuang0403/COMP367_Assignment3_Q1.git'
      }
    }

    stage('Build maven project') {
      steps {
        sh 'mvn -version'
        sh 'mvn clean package'
      }
    }

    stage('Docker login') {
      steps {
        sh 'docker login -u hzyxby1996 -p ${DOCKERHUB_PWD}'
      }
    }

    stage('Docker build') {
      steps {
        sh 'docker build -t ${IMAGE_NAME} .'
      }
    }

    stage('Docker push') {
      steps {
        sh 'docker push ${IMAGE_NAME}'
      }
    }
  }

  post {
    success {
      archiveArtifacts artifacts: 'target/*.war', fingerprint: true
    }
  }
}
