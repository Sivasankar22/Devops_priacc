pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "📥 Pulling code from GitHub via SSH..."
                git branch: 'main',
                    url: 'git@github.com:Sivasankar22/Devops_priacc.git',
                    credentialsId: 'github-ssh'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build Artifact') {
            steps {
                sh 'zip -r build.zip app.js package.json test.js'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build.zip', fingerprint: true
            }
        }
        stage('Notify') {
            steps {
                echo "✅ Build and tests successful! (Mock Slack/Email notification)"
            }
        }
    }

    post {
        failure {
            echo "❌ Build failed. Please check logs."
        }
    }
}
