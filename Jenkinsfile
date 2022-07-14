pipeline {
    agent any
    environment {
      DOCKERHUB_CREDENTIALS = credentials('docker-hub-rusucristian')
      REGISTRY_NAME = "rusucristian/nodejs-test"
    }
    stages {
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/rusucristian/nodejs-test.git'
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t $REGISTRY_NAME:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push $REGISTRY_NAME:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
