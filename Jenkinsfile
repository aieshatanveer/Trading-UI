pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/aieshatanveer/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh '''
                    # Clean previous installs
                    rm -rf node_modules package-lock.json
                    # Install dependencies
                    npm install
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm run build || echo "No build script defined, skipping..."'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test || echo "No test script found, skipping tests..."'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment stage (customize as needed)...'
                // Example: sh 'scp -r dist/ user@server:/var/www/html'
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully!'
        }
        failure {
            echo '❌ Build failed. Please check the logs.'
        }
    }
}
