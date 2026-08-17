pipeline {
    agent {
        docker {
            //image 'node:18-alpine'
            image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
            steps {
                //clearWs()
                sh '''
                   ls -la
                   node --version
                   npm --version
                   npm ci
                   npm run build
                   ls -la
                   npm test
                '''
            }
        }

        stage('E2E') {
            steps {
                sh '''
                   npm install serve
                   node_modules/.bin/serve -s build & sleep 10
                   npx playwright test --reporter=html
                '''
            }
        }
    }

    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
}