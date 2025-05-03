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
                sh 'which docker || echo "Docker not found in PATH"'
                sh 'docker --version || echo "Docker not working"'
                sh 'docker compose version || echo "Docker Compose not working or not installed properly"'

                echo 'Building and running static site with Docker Compose...'
                sh 'docker compose down || echo "Failed to run docker compose down"'
                sh 'docker compose up -d --build || echo "Failed to run docker compose up"'
            }
        }
    }

    post {
        success {
            echo 'Deployment Success'
        }
        failure {
            echo 'Deployment Failed'
        }
    }
}
