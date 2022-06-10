pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerID001')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/sbk002/nodejs-wokring.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t balanodejs/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push balanodejs/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

