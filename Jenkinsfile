pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Checkout code from Git
                    git 'https://github.com/Parameswaran009/ArgoCD_Project.git'
                }
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build Docker image
                    dockerImage = docker.build("parameswaran009/argocd-project:${env.BUILD_ID}")

                    // Push the Docker image to Docker Hub
                    dockerImage.push()
                }
            }
        }
    }
}

