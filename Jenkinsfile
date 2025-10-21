pipeline {
    agent any

    environment {
        IMAGE_NAME = "aakashthapliyal/portfolio"
        CONTAINER_NAME = "portfolio-container"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/AakashThapliyal/sem3minorproject.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Run Container Locally') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                docker run -d -p 8080:80 --name $CONTAINER_NAME $IMAGE_NAME:latest
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
