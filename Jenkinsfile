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

                    /ArgoCD_Projeco/ Build Docker image
                    sh "docker build -t ${params.DOCKER_USERNAME}/nodejs-docker-jenkins-argo-project ."
                }
            }
        }

        stage('Push to Docker Registry') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    sh "docker push ${params.DOCKER_USERNAME}/nodejs-docker-jenkins-argo-project"
                }
            }
        }
    }
}

