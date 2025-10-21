pipeline {
    agent any

    environment {
        IMAGE_NAME = "aakashthapliyal/portfolio"
        CONTAINER_NAME = "portfolio-container"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/AakashThapliyal/sem3minorproject.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Run Container Locally') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || echo "No existing container"
                docker rm %CONTAINER_NAME% || echo "No existing container"
                docker run -d -p 8080:80 --name %CONTAINER_NAME% %IMAGE_NAME%:latest
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Portfolio Deployed Successfully on Local Docker!'
        }
        failure {
            echo '❌ Build/Deploy Failed!'
        }
    }
}
