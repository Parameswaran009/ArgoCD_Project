pipeline {
    agent any

    parameters {
        string(name: 'DOCKER_USERNAME', defaultValue: 'parameswarankrishnan36@gmail.com', description: 'Docker Hub Username')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Checkout code from Git
                    checkout scm

                    // Build Docker image
                    sh "docker build -t ${params.DOCKER_USERNAME}/nodejs-docker-jenkins-argo ."
                }
            }
        }

        stage('Push to Docker Registry') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    sh "docker push ${params.DOCKER_USERNAME}/nodejs-docker-jenkins-argo"
                }
            }
        }
    }
}

