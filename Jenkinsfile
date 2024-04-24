pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Clean and install dependencies
                    sh 'npm ci'

                  
                  // Build Angular project
                    sh 'ng build'
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Example Docker build command
                    docker.build('my-docker-image:latest', '.')
                }
            }
        }
        stage('Deploy to AWS') {
            environment {
                AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
                AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
                AWS_DEFAULT_REGION = 'us-east-1' // Update with your AWS region
            }
            steps {
                script {
                    // Deploy Docker containers using docker-compose
                    docker.withRegistry('https://example-registry-url.com', 'docker-registry-credentials') {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }
}
