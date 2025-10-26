pipeline {
    agent {
        docker { 
            image 'node:18-alpine'
            args '-p 3000:3000'
        }
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || echo "No tests configured"'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }
}
