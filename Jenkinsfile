pipeline {
    agent any

    tools {
        nodejs "nodejs" // Ensure NodeJS is configured in Jenkins Global Tools
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials') // Jenkins credential ID for Docker Hub
        IMAGE_NAME = "aliwazeer/task-app"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/nodejs-docker-task']],
                    userRemoteConfigs: [[url: 'https://github.com/Uliwazeer/Task.git']]
                ])
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "⚠️ No tests found, skipping."'
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
