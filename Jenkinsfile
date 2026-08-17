pipeline {
    agent any

    stages {

        stage('Clone Source Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Package Application') {
            steps {
                sh 'tar -czf application.tar.gz --exclude=.git --exclude=application.tar.gz .'
            }
        }

        stage('Deliver Artifact') {
            steps {
                archiveArtifacts artifacts: 'application.tar.gz',
                                  fingerprint: true
            }
        }
    }
}
