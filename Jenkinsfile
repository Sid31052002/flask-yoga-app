pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                script {
                    // Create a virtual environment and install dependencies
                    sh '''
                        python3 -m venv venv
                        . venv/bin/activate
                        pip install -r requirements.txt
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    // Run tests using the virtual environment
                    sh '''
                        . venv/bin/activate
                        pytest
                    '''
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh '''
                        . venv/bin/activate
                        docker build -t flask-yoga-app .
                    '''
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    // Deploy the application
                    sh '''
                        . venv/bin/activate
                        docker run -d -p 5000:5000 flask-yoga-app
                    '''
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline execution completed!'}
        failure {
            echo 'Deployment failed.'}
}}