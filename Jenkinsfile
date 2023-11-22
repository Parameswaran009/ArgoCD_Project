pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Checkout code from Git
                    checkout scm

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
