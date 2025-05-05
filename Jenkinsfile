pipeline {
    agent any

    stages {
        stage('Cloning Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/GujjuChandini/weather.git'
            }
        }

        stage('Deployment') {
            steps {
                echo 'Checking Docker and Docker Compose environment...'
                sh 'whoami'
                sh 'docker --version || echo "Docker not working"'
                sh 'docker compose version || docker-compose --version || echo "Compose not working"'

                echo 'Building and running static site with Docker Compose...'
                sh 'docker compose down || docker-compose down || echo "Failed to bring down"'
                sh 'docker compose up -d --build || docker-compose up -d --build || echo "Failed to bring up"'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Success'
        }
        failure {
            echo '❌ Deployment Failed'
        }
    }
}
