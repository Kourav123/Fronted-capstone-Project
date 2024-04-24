pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Set up environment to use Angular CLI and Node.js
                  //  def npmHome = tool name: 'NodeJS 18', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                  //  env.PATH = "${npmHome}/bin:${env.PATH}"

                    // Install npm dependencies
                    sh 'npm ci'

                    // Install Angular CLI (if not already installed)
                    sh 'npm config set prefix ~/.npm-global'
                       sh 'export PATH=~/.npm-global/bin:$PATH'
                      sh 'npm install -g @angular/cli'


                    // Build Angular project
                   sh 'ng build'
                }
            }
        }
      stage("run the docker containers"){
            steps{
                sh "docker-compose down"
                sh "docker-compose up --build -d"       
            }
        }
        stage("Check images and runnign containers"){
            steps{
                sh "docker images"
                sh "docker ps"       
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
