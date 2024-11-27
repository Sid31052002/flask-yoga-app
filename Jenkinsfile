pipeline {
    agent any

    environment {
        // Define environment variables
        PROJECT_DIR = "flask-yoga-app"
        DEPLOY_SERVER = "172.20.0.223"  // Your local system's IP address
        DEPLOY_USER = "adarsh16"        // Your local system username
        DEPLOY_PATH = "/home/adarsh16/yoga-app"  // Your deployment folder path
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Sid31052002/flask-yoga-app'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source venv/bin/activate
                pytest
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t yoga-pose-app:latest .
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sshagent(['jenkins-ssh-credentials']) {
                    sh '''
                    scp docker-compose.yml ${DEPLOY_USER}@${DEPLOY_SERVER}:${DEPLOY_PATH}
                    ssh ${DEPLOY_USER}@${DEPLOY_SERVER} "cd ${DEPLOY_PATH} && docker-compose down && docker-compose up -d"
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed!'
        }
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed.'}
    }
}
