pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('VERCEL_TOKEN') // Jenkins credential ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Pull the latest code from GitHub
                git branch: 'main', url: 'https://github.com/salman-281/project-2.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing Node.js dependencies..."
                sh 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                echo "Building Next.js project..."
                sh 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                echo "Deploying to Vercel..."
                // Use your token to deploy to Vercel
                sh 'npx vercel --prod --token $VERCEL_TOKEN --confirm'
            }
        }
    }

    post {
        success {
            echo "Deployment succeeded! 🎉"
        }
        failure {
            echo "Deployment failed! ❌"
        }
    }
}
