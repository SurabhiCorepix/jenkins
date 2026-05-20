pipeline {
    agent any

    environment {
        REPO_NAME = "jenkins"

        GIT_URL = "https://github.com/SurabhiCorepix/jenkins.git"

        CLONE_DIR = "/opt/jenkins/${REPO_NAME}"

        APP_DIR = "/opt/cp_apps/${REPO_NAME}"
    }

    stages {

        stage('Prepare Folders') {
            steps {
                sh '''
                mkdir -p /opt/jenkins
                mkdir -p /opt/cp_apps
                '''
            }
        }

        stage('Clone or Pull Repository') {
            steps {
                sh '''
                set -ex

                if [ -d "$CLONE_DIR/.git" ]; then
                    echo "Repository already exists. Pulling latest code..."

                    cd $CLONE_DIR
                    git pull origin main

                else
                    echo "Cloning fresh repository..."

                    git clone $GIT_URL $CLONE_DIR
                fi
                '''
            }
        }

        stage('Copy Project to App Folder') {
            steps {
                sh '''
                set -ex

                mkdir -p $APP_DIR

                rsync -av $CLONE_DIR/ $APP_DIR/

                echo "Project synced successfully"
                '''
            }
        }

        stage('Verify Files') {
            steps {
                sh '''
                ls -la $APP_DIR
                '''
            }
        }

        stage('Check Node & NPM') {
            steps {
                sh '''
                node -v
                npm -v
                '''
            }
        }

        stage('NPM Install') {
            steps {
                sh '''
                set -ex

                cd $APP_DIR

                npm install
                '''
            }
        }

        stage('NPM Build') {
            steps {
                sh '''
                set -ex

                cd $APP_DIR

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