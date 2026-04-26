pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t juice-shop-devsecops .'
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running container...'
                sh 'docker rm -f juice-shop || true'
                sh 'docker run -d -p 3000:3000 --name juice-shop juice-shop-devsecops'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
