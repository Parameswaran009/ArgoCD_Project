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

        stage('Pull Source Code - clmn-admin-app') { // New Stage
            steps {
                dir("${env.JOB_BASE_NAME}") {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/man']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [[$class: 'CleanCheckout']],
                        submoduleCfg: [],
                        userRemoteConfigs: [[credentialsId: 'Parameswaran009', url: 'https://github.com/Parameswaran009/ArgoCD_Project']]
                    ])
                    sh 'git rev-parse HEAD > commit'
                    script {
                        COMMIT_ID = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
                        echo "COMMIT_ID>>>: ${COMMIT_ID}"
                        COMMIT_ID = "${COMMIT_ID}"
                    }
                    sh 'echo $COMMIT_ID'
                    echo "$COMMIT_ID"
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

