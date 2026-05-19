pipeline {
    agent any

    environment {
        DEST_DIR = "/opt/jenkins"
    }

    stages {

        stage('Git Pull') {
            steps {
                git branch: 'main',
                url: 'https://github.com/SurabhiCorepix/jenkins.git'
            }
        }

        stage('Copy Latest Code') {
            steps {
                sh """
                set -e
                mkdir -p $DEST_DIR

                cp -r ${WORKSPACE}/* $DEST_DIR/
                """
            }
        }

        stage('Install Dependencies (npm install)') {
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

        stage('Verify Files') {
            steps {
                sh """
                echo "Files copied successfully"
                ls -la $DEST_DIR
                """
            }
        }

    }

    post {
        success {
            echo "✅ SUCCESS: Build completed"
        }

        failure {
            echo "❌ FAILED: Check logs above"
        }
    }
}