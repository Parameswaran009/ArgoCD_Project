pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "your-docker-username/nodejs-docker-image"
        DOCKER_HUB_CREDENTIALS = 'your-dockerhub-credentials-id'
        GIT_CREDENTIALS = 'git-credentials-id'
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Checkout code from Git with credentials
                    withCredentials([usernamePassword(credentialsId: GIT_CREDENTIALS, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        git credentialsId: 'git-credentials-id', url: 'https://github.com/Parameswaran009/ArgoCD_Project.git', branch: 'main'
                    }
                }
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build Docker image
                    def dockerImage = docker.build("${DOCKER_IMAGE_NAME}:${env.BUILD_ID}")

                    // Push the Docker image to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CREDENTIALS) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}


