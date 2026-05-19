pipeline {
    agent any

    environment {
        DEST_DIR = "/opt/jenkins"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/SurabhiCorepix/jenkins.git'
            }
        }

        stage('Copy Code') {
            steps {
                sh """
                set -e
                mkdir -p $DEST_DIR
                cp -r ${WORKSPACE}/* $DEST_DIR/
                """
            }
        }

        stage('Install Dependencies (npm i)') {
            steps {
                dir("$DEST_DIR") {
                    sh """
                    set -e
                    echo "Installing dependencies..."
                    npm install
                    """
                }
            }
        }

        stage('Build Project (npm build)') {
            steps {
                dir("$DEST_DIR") {
                    sh """
                    set -e
                    echo "Building project..."
                    npm run build
                    """
                }
            }
        }

    }

    post {
        success {
            echo "✅ Pipeline SUCCESS: Build completed"
        }

        failure {
            echo "❌ Pipeline FAILED: Check logs above"
        }
    }
}