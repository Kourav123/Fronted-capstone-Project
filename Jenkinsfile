pipeline {
    agent any

    stages {
        stage('Prepare Environment') {
            steps {
                // Verify Node.js and npm versions
                sh 'node --version'
                //sh 'npm --version'

                // Install Angular CLI globally
                sh 'npm install -g @angular/cli'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Clean and install dependencies
                    sh 'npm ci'

                    // Build Angular app for production
                    sh 'ng build --prod'
                }
            }
        }

        // Add Docker Build and Deploy to AWS stages as needed
    }
}
