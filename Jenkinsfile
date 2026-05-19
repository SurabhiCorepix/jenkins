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

        stage('Copy Code to /opt/jenkins') {
            steps {
                sh """
                set -e

                echo "Creating destination folder..."
                mkdir -p $DEST_DIR

                echo "Copying code..."
                cp -r ${WORKSPACE}/* $DEST_DIR/
                """
            }
        }

        stage('npm install in /opt/jenkins') {
            steps {
                sh """
                set -e

                echo "Running npm install in /opt/jenkins"
                cd $DEST_DIR

                npm install
                """
            }
        }

        stage('npm build in /opt/jenkins') {
            steps {
                sh """
                set -e

                echo "Running npm build in /opt/jenkins"
                cd $DEST_DIR

                npm run build
                """
            }
        }

        stage('Verify') {
            steps {
                sh """
                echo "Build completed successfully"
                ls -la $DEST_DIR
                """
            }
        }

    }

    post {
        success {
            echo "✅ SUCCESS: Full pipeline completed"
        }

        failure {
            echo "❌ FAILED: Check logs above"
        }
    }
}