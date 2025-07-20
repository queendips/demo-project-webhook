pipeline {
    agent any

    triggers {
        githubPush() // Enables webhook triggering
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/demo-project-webhook.git'
            }
        }

        stage('Build') {
            steps {
                echo '🔧 Building the project...'
                sh './build.sh' // Make sure this file exists and is executable
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh './test.sh' // Make sure this file exists and is executable
            }
        }

        stage('Run') {
            steps {
                echo '🚀 Running the application...'
                sh './run.sh' // Make sure this file exists and is executable
            }
        }
    }

    post {
        success {
            echo '✅ Build, test, and run steps completed successfully.'
        }
        failure {
            echo '❌ One or more steps failed.'
        }
    }
}
