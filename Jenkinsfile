pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                // Specify the correct branch 'main' here
                git branch: 'main', url: 'https://github.com/Sid31052002/flask-yoga-app.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Install dependencies if required, for example:
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image if necessary
                sh 'docker build -t flask-yoga-app .'
            }
        }

        stage('Deploy Application') {
            steps {
                // Deploy your application here
                sh 'docker run -d -p 5000:5000 flask-yoga-app'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed!'
        }
        failure {
            echo 'Deployment failed.'}
            }
}