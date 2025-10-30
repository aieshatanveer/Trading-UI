pipeline {
    agent any

    tools {
        nodejs "NodeJS-20" // Make sure this name matches Jenkins Tool Configuration
    }

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

                    echo "Node version in use:"
                    node -v
                    npm -v

                    echo "Installing dependencies..."
                    # Use --force to bypass peer dependency conflicts
                    npm install --force
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    echo "Building the project..."
                    # Disable CI mode to prevent interactive failures
                    CI=false npm run build
                '''
            }
        }

        stage('Post Build') {
            steps {
                echo 'Build completed successfully!'
            }
        }
    }

    post {
        failure {
            echo 'Build failed. Please check Jenkins console output for details.'
        }
    }
}
