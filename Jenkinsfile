pipeline {
    agent any

    environment {
        DOCKER_BUILDKIT = '1'
    }

    stages {
        stage('Checkout') {
            steps {
                echo '📦 Checking out the repository...'
                checkout scm
            }
        }

        stage('Deployment') {
            steps {
                echo '🔍 Checking Docker environment and deploying...'
                sh '''
                    echo 👤 User: $(whoami)
                    echo 🐳 Docker version:
                    docker --version
                    echo 🐳 Docker Compose version:
                    docker compose version

                    echo 🧹 Stopping existing containers (if any)...
                    docker compose down || true

                    echo 🚀 Starting deployment using Docker Compose...
                    docker compose up -d --build
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
