pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "mern-backend"
        FRONTEND_IMAGE = "mern-frontend"
    }

    stages {

        stage('Clone repo') {
            steps {
                git 'https://github.com/mhdnisham/Mern-use-app.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t $BACKEND_IMAGE .'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('frontend') {
                    sh 'docker build -t $FRONTEND_IMAGE .'
                }
            }
        }

        stage('Stop Running Containers') {
            steps {
                sh 'docker rm -f backend-container || true'
                sh 'docker rm -f frontend-container || true'
            }
        }

        stage('Run Backend') {
            steps {
                sh 'docker run -d -p 5000:5000 --name backend-container mern-backend'
            }
        }

        stage('Run Frontend') {
            steps {
                sh 'docker run -d -p 3000:3000 --name frontend-container mern-frontend'
            }
        }

    }

    post {
        success {
            echo "Deployment Successful 🚀"
        }
        failure {
            echo "Build Failed ❌"
        }
    }
}
