pipeline {
    agent any

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh 'echo "🧹 Workspace cleaned before pipeline run."'
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/queendips/demo-project-webhook.git']]
                ])
            }
        }

        stage('Build') {
            steps {
                script {
                    try {
                        echo "🔨 Building the application..."
                        sh 'chmod +x build.sh'
                        sh './build.sh'
                    } catch (err) {
                        echo "❌ Build failed: ${err}"
                        currentBuild.result = 'FAILURE'
                        error("Stopping pipeline due to build failure.")
                    }
                }
            }
        }

        stage('Unit Testing') {
            steps {
                sh '''
                echo "🧪 Running Unit Tests..."
                # Add your test logic here, or run a test script if available
                '''
            }
        }

        stage('Deploy to Dev and QA') {
            when {
                branch 'develop'
            }
            steps {
                sh 'echo "Building for Dev and QA environments..."'
                sh 'echo "Deploying to Dev..."'
                sh 'echo "Deploying to QA..."'
            }
        }

        stage('Deploy to Staging and Pre-Prod') {
            when {
                branch 'main'
            }
            steps {
                sh 'echo "Building for Staging and Pre-Prod..."'
                sh 'echo "Deploying to Staging..."'
                sh 'echo "Deploying to Pre-Prod..."'
            }
        }
    }
}
