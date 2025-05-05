pipeline {
    agent any

    stages {
        stage('Cloning Repository') {
            steps {
                echo '📥 Cloning the repository...'
                git branch: 'main', url: 'https://github.com/GujjuChandini/weather.git'
            }
        }

        stage('Deployment') {
            steps {
                echo '🔍 Checking Docker and Docker Compose environment...'
                sh '''
                    echo "👤 Running as: $(whoami)"
                    docker --version || echo "⚠️ Docker is not installed or not working"
                    
                    if command -v docker-compose &> /dev/null; then
                        echo "✅ Using docker-compose"
                        COMPOSE_CMD="docker-compose"
                    elif docker compose version &> /dev/null; then
                        echo "✅ Using docker compose"
                        COMPOSE_CMD="docker compose"
                    else
                        echo "❌ Neither docker-compose nor docker compose is available"
                        exit 1
                    fi

                    echo "🛑 Stopping any existing containers..."
                    $COMPOSE_CMD down || echo "⚠️ Failed to stop containers"

                    echo "🚀 Building and starting containers..."
                    $COMPOSE_CMD up -d --build || echo "❌ Failed to start containers"
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
