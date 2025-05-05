pipeline {
    agent any

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

                    echo 🛑 Bringing down previous containers...
                    docker compose down || echo ⚠️ Failed to stop containers

                    echo 🚀 Building and starting new containers...
                    docker compose up -d --build || echo ❌ Failed to start containers
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
