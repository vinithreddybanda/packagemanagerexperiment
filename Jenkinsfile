pipeline {
    agent any
    environment {
            DOCKERHUB_USER = 'vinithreddybanda' // Replace with your Docker Hub username
            DOCKERHUB_TOKEN = credentials('dockerhub-creds') // Docker Hub token from Jenkins credentials
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
                    sh "docker build -t ${DOCKERHUB_USER}/${IMAGE_NAME}:latest ."
                }
            }
            stage('Login to Docker Hub') {
                steps {
                    sh "echo $DOCKERHUB_TOKEN | docker login -u $DOCKERHUB_USER --password-stdin"
                }
            }
            stage('Push Image to Docker Hub') {
                steps {
                    sh "docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:latest"
                }
            }
    }
    post {
        always {
            cleanWs()
        }
    }
}