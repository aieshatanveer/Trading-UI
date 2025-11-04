pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/aieshatanveer/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "No tests defined"'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Node.js app...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                # Example: run your app
                sh 'nohup node app.js > output.log 2>&1 &'
            }
        }
    }
}
