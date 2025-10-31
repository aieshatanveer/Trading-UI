pipeline {
    agent any

    tools {
        nodejs 'NodeJS-20'   // Make sure this matches your NodeJS tool name in Jenkins
    }

    environment {
        PATH = "$PATH:/usr/local/bin"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/aieshatanveer/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                timeout(time: 60, unit: 'MINUTES') {   // Increased timeout from 30 → 60 mins
                    sh '''
                        echo "Cleaning old modules..."
                        rm -rf node_modules package-lock.json
                        echo "Installing dependencies..."
                        npm ci || npm install --force
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                sh '''
                    echo "Building project..."
                    npm run build
                '''
            }
        }

        stage('Post Build') {
            steps {
                echo 'Build successful! Ready for deployment.'
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed. Check logs for errors.'
        }
        success {
            echo '✅ Pipeline completed successfully!'
        }
        aborted {
            echo '⚠️ Build aborted due to timeout or manual stop.'
        }
    }
}
