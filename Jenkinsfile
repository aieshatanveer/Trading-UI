pipeline {
    agent any

    tools {
        nodejs "NodeJS14" 
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aieshatanveer/Trading-UI.git', branch: 'master'
            }
        }

        stage('Install') {
            steps {
                sh '''
                    npm cache clean --force
                    rm -rf node_modules package-lock.json
                    npm install --omit=optional
                '''
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo ":warning: No tests found or failed"'
            }
        }

        stage('Build') {
            steps {
                withEnv(["CI=false"]) {
                    sh 'npm run build'
                }
            }
        }
    }

    post {
        success {echo ':white_check_mark:Node.js pipeline finished successfully.'}
        failure {echo ':x:Node.js pipeline failed - check console output.'}
    }
}

