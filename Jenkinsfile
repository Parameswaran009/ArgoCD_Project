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

        stage('Build') {
            steps {
                script {
                    // Build Docker image
                    sh 'docker build -t parameswaran009/argocd-project .'
                }
            }
        }

        stage('Push to Docker Registry') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    sh 'docker push parameswaran009/argocd-project'
                }
            }
        }
    }
}

