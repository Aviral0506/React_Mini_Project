pipeline {
    agent any

    triggers {
        githubPush()
    }

    environment {
        IMAGE_NAME = 'timer'
    }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Lint') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('Build application') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Build Docker image') {
            steps {
                sh 'docker build --tag "$IMAGE_NAME:${BUILD_NUMBER}" --tag "$IMAGE_NAME:latest" .'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
