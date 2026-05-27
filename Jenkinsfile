pipeline {
    agent any

    environment {
        IMAGE_NAME = "nt_jk_app"
        CONTAINER_NAME = "nt_jk_container"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Stop Old Container') {
            steps {
                sh """
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                sh """
                docker run -d \
                --name ${CONTAINER_NAME} \
                -p 3000:3000 \
                ${IMAGE_NAME}
                """
            }
        }
    }

    post {
        success {
            echo 'Docker deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}