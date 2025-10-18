pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Yuvakunaal/DevOps-Assignment-2.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh '/usr/local/bin/docker build -t devops-assignment-2-app .'
            }
        }
        
        stage('Test Application') {
            steps {
                sh '''
                # Clean up any existing containers first
                /usr/local/bin/docker stop test-app 2>/dev/null || true
                /usr/local/bin/docker rm test-app 2>/dev/null || true
                
                # Run test container
                /usr/local/bin/docker run -d --name test-app -p 8001:8000 devops-assignment-2-app
                sleep 10
                curl -f http://localhost:8001 || exit 1
                /usr/local/bin/docker stop test-app
                /usr/local/bin/docker rm test-app
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