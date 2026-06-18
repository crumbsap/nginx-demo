pipeline {
    agent any

    environment {
        IMAGE_NAME = "nginx-demo"
        CONTAINER_NAME = "nginx-demo-container"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat '''
                docker rm -f %CONTAINER_NAME%
                exit /b 0
                '''
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 8081:80 --name %CONTAINER_NAME% %IMAGE_NAME%'
            }
        }

        stage('Verify') {
            steps {
                bat 'docker ps'
            }
        }

    }
}