pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Clone Source Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build Application') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

        stage('Package Application') {
            steps {
                bat '''
                if not exist package mkdir package
                powershell -NoProfile -Command "Compress-Archive -Path * -DestinationPath package\\application.zip -Force"
                '''
            }
        }

        stage('Deliver Artifact') {
            steps {
                archiveArtifacts artifacts: 'package/application.zip', fingerprint: true
            }
        }
    }
}
