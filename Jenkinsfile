groovy
pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds') // Jenkins credentials ID
        DOCKERHUB_USER = 'vinithreddybanda' // Replace with your Docker Hub username
        IMAGE_NAME = "my-web-app"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKERHUB_USER}/${IMAGE_NAME}:latest")
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_USER --password-stdin"
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    dockerImage.push()
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}