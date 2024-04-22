pipeline {
    agent any
    stages {
        stage("run the docker"){
            steps{
                sh "docker-compose down"
		        sh "docker-compose up --build -d"
		        sh "docker ps"
     	       }
        }
    }    
}