pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "parameswaran009/argocd-project"
        DOCKER_HUB_CREDENTIALS = 'dockerhub-credentials-id'
        GIT_CREDENTIALS = 'git-credentials-id'
        GIT_TOOL = 'Default'
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Checkout code from Git with credentials
                    withCredentials([usernamePassword(credentialsId: GIT_CREDENTIALS, usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                        git tool: GIT_TOOL, credentialsId: 'git-credentials-id', url: 'https://parameswaran009:Parameswaran@123@github.com/Parameswaran009/ArgoCD_Project.git', branch: 'main'
                    }
                }
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Build Docker image
                    def dockerImage = docker.build("${DOCKER_IMAGE_NAME}:${env.BUILD_ID}")

                    // Push the Docker image to Docker Hub with credentials
                    withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS, usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                        docker.withRegistry('https://registry.hub.docker.com', 'DOCKER_HUB_USERNAME', 'DOCKER_HUB_PASSWORD') {
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}

