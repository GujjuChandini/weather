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
                    # Ensure the script is run in bash
                    /bin/bash -c "echo 👤 User: $(whoami)"
                    /bin/bash -c "echo 🐳 Docker version: $(docker --version)"
                    /bin/bash -c "echo 🐳 Docker Compose version: $(docker-compose --version)"

                    /bin/bash -c "echo 🧹 Stopping existing containers (if any)..."
                    /bin/bash -c "docker-compose down || true"

                    /bin/bash -c "echo 🚀 Starting deployment using Docker Compose..."
                    /bin/bash -c "docker-compose up -d --build"
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
