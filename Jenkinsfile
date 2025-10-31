pipeline {
    agent any

    tools {
        nodejs 'NodeJS_20' // The name you configured under "Manage Jenkins" → "Global Tool Configuration"
    }

    environment {
        VERCEL_TOKEN = credentials('VERCEL_TOKEN') // Jenkins credential ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Checking out code from GitHub..."
                git branch: 'main', url: 'https://github.com/salman-281/project-2.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing Node.js dependencies..."
                bat 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                echo "Building Next.js project..."
                bat 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                echo "Deploying to Vercel..."
                bat 'npx vercel --prod --token %VERCEL_TOKEN% --confirm'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment succeeded! 🎉"
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}
