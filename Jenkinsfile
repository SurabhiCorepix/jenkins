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

        stage('Prepare Folder') {
            steps {
                sh '''
                set -e
                mkdir -p /opt/jenkins
                '''
            }
        }

        stage('Copy Code') {
            steps {
                sh '''
                set -e
                echo "Copying code to /opt/jenkins"

                cp -r ${WORKSPACE}/* $DEST_DIR/
                '''
            }
        }

        stage('Install Dependencies (npm install)') {
            steps {
                dir("${env.DEST_DIR}") {
                    sh '''
                    set -e
                    echo "Running npm install"

                    npm install
                    '''
                }
            }
        }

        stage('Build Project (npm run build)') {
            steps {
                dir("${env.DEST_DIR}") {
                    sh '''
                    set -e
                    echo "Running npm build"

                    npm run build
                    '''
                }
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