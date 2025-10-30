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
                sh '''
                    echo "Cleaning old modules..."
                    rm -rf node_modules package-lock.json
                    echo "Installing dependencies..."
                    npm install
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    echo "Building the project..."
                    CI=false npm run build
                '''
            }
        }

        stage('Post Build') {
            steps {
                echo '✅ Build completed successfully!'
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed. Please check Jenkins console output for errors.'
        }
    }
}
