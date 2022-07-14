pipeline {
    agent any
    environment {
      DOCKERHUB_CREDENTIALS = credentials('docker-hub-rusucristian')
      REGISTRY_NAME = "rusucristian/nodejs-test"
      NEXT_VERSION = "1.0"
    }
    stages {
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/rusucristian/nodejs-test.git'
            }
        }

        stage('Build docker image') {
            steps {
                sh "docker build -t ${REGISTRY_NAME}:${NEXT_VERSION} ."
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh "docker push ${REGISTRY_NAME}:${NEXT_VERSION}"
            }
        }
    }

    post {
      always {
        sh 'docker logout'
        sh "docker rmi -f ${REGISTRY_NAME}:${NEXT_VERSION}"
      }
    }
}
