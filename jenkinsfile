pipeline {
    agent any

    stages {
        stage('Cloning Repository') {
            steps {
                git 'https://github.com/GujjuChandini/weather.git'
            }
        }

        stage('Deployment') {
            steps {
                echo 'Building and running static site with Docker Compose...'
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
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
