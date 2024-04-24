pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Clean and install dependencies
                    sh 'npm ci'

                    // Build Angular app for production
                   // Set up environment to use Angular CLI
                    def npmHome = tool name: 'NodeJS 14', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${npmHome}/bin:${env.PATH}"
                    sh 'ng build'  // Execute ng build command
                }
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    // Build Docker image
                    docker.build('angular-app:latest', '.')

                    // Optionally, you can push the image to a Docker registry here
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
