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
                    echo 🐳 Checking Docker versions...
                    docker --version
                    docker compose version

                    echo 🚀 Starting deployment using docker compose...
                    docker compose down || true
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
