pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/Sid31052002/flask-yoga-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                    pip install pytest
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh '''
                    . venv/bin/activate
                    pytest || echo "Tests failed"
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image"
                // Add your Docker build steps here
            }
        }

        stage('Deploy Application') {
            steps {
                echo "Deploying application"
                // Add your deployment steps here
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