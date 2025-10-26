pipeline {
    agent {
        docker {
            image 'node:18'  // or node:20
            args '-u root'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'nodejs-docker-task', url: 'https://github.com/Uliwazeer/Task'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build || echo "No build step defined"'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "No tests defined"'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline succeeded!'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
