pipeline {
    agent any
    environment {
        PATH = "${PATH}:/var/lib/jenkins/.local/bin"  // Add this line to include the local bin directory
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Sid31052002/flask-yoga-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'  // This will now work as pytest is in the PATH
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-yoga-app .'
            }
        }

        stage('Deploy Application') {
            steps {
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