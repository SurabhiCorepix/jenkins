pipeline {
    agent any

    environment {
        DEST_DIR = "C:\Users\Lenovo\Documents\CorepixGit\jenkins\extra_folder"
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
                mkdir -p $DEST_DIR

                cp -r ${WORKSPACE}/* $DEST_DIR/
                """
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
}