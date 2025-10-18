pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/DevOps-Assignment-2.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-assignment-2-app .'
            }
        }
        
        stage('Test Application') {
            steps {
                sh '''
                docker run -d --name test-app -p 8000:8000 devops-assignment-2-app
                sleep 10
                curl -f http://localhost:8000 || exit 1
                docker stop test-app
                docker rm test-app
                '''
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}