pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Clone source code...'
            }
        }

        stage('Install') {
            steps {
                echo 'Install dependencies...'
                bat 'npm install'
            }
        }

        stage('Run') {
            steps {
                echo 'Run application...'
                bat 'node app.js'
            }
        }
    }
}