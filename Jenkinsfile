pipeline {
    agent any

    environment {
        IMAGE_NAME = "nt_jk_app"
        CONTAINER_NAME = "nt_jk_container"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting source code...'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Stop Old Container') {
            steps {
                bat """
                docker stop %CONTAINER_NAME% || exit 0
                docker rm %CONTAINER_NAME% || exit 0
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                bat """
                docker run -d ^
                --name %CONTAINER_NAME% ^
                -p 3000:3000 ^
                %IMAGE_NAME%
                """
            }
        }
    }

    post {
        success {
            echo 'Docker container deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}