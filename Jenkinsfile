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

        stage('Check Node & NPM') {
            steps {
                sh '''
                echo "Checking Node..."
                node -v

                echo "Checking NPM..."
                npm -v
                '''
            }
        }

        stage('Clean Old Files') {
            steps {
                sh '''
                rm -rf /opt/jenkins/*
                '''
            }
        }

        stage('Copy Code') {
            steps {
                sh '''
                set -ex

                mkdir -p /opt/jenkins

                cp -r ${WORKSPACE}/* /opt/jenkins/

                echo "Files copied successfully"
                '''
            }
        }

        stage('Verify Files') {
            steps {
                sh '''
                ls -la /opt/jenkins
                '''
            }
        }

        stage('NPM Install') {
            steps {
                sh '''
                set -ex

                cd /opt/jenkins

                npm install
                '''
            }
        }

        stage('NPM Build') {
            steps {
                sh '''
                set -ex

                cd /opt/jenkins

                npm run build
                '''
            }
        }

    }

    post {

        success {
            echo '✅ PIPELINE SUCCESS'
        }

        failure {
            echo '❌ PIPELINE FAILED'
        }

        always {
            echo 'Pipeline Finished'
        }
    }
}