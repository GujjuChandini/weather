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
                echo '🔍 Checking Docker environment and deploying...'
                sh '''
                    echo "👤 User: $(whoami)"
                    docker --version
                    docker compose version || docker-compose --version

                    # Use docker compose (plugin) first; fallback to docker-compose (binary)
                    if docker compose version &> /dev/null; then
                        COMPOSE="docker compose"
                    elif command -v docker-compose &> /dev/null; then
                        COMPOSE="docker-compose"
                    else
                        echo "❌ Neither docker compose nor docker-compose is available!"
                        exit 1
                    fi

                    echo "🛑 Bringing down previous containers..."
                    $COMPOSE down || echo "⚠️ Failed to stop containers"

                    echo "🚀 Building and starting new containers..."
                    $COMPOSE up -d --build || echo "❌ Failed to start containers"
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
