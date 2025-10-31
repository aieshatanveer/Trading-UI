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
                timeout(time: 30, unit: 'MINUTES') { // allows npm install up to 30 mins
                    sh '''
                        echo "Cleaning old modules..."
                        rm -rf node_modules package-lock.json

                        echo "Installing dependencies..."
                        npm install --force
                    '''
                }
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

