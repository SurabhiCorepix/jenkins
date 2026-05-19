pipeline {
    agent any

    environment {
        DEST_DIR = "C:\\Users\\Lenovo\\Documents\\CorepixGit\\jenkins\\extra_folder"
    }

    stages {

        stage('Checkout Code (Git Pull)') {
            steps {
                git branch: 'main',
                url: 'https://github.com/SurabhiCorepix/jenkins.git'
            }
        }

        stage('Test') {
            steps {
                echo 'Jenkins working'
            }
        }

        stage('Copy to Extra Folder') {
            steps {
                bat """
                if not exist "%DEST_DIR%" mkdir "%DEST_DIR%"

                robocopy "%WORKSPACE%" "%DEST_DIR%" /E /R:2 /W:2
                """
            }
        }

        stage('Verify Copy') {
            steps {
                bat """
                dir "%DEST_DIR%"
                """
            }
        }

    }
}