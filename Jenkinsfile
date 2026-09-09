pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-cicd-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop devops-cicd-container || true
                    docker rm devops-cicd-container || true
                    docker run -d --name devops-cicd-container -p 5000:5000 devops-cicd-app
                '''
            }
        }

        stage('Verify Application') {
            steps {
                sh 'sleep 3'
                sh 'curl -f http://localhost:5000'
            }
        }
    }
}
