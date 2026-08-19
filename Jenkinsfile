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
                sh 'echo "No external dependencies required for this project"'
            }
        }

        stage('Build Application') {
            steps {
                sh '''
                    mkdir -p build
                    cp Jenkinsfile build/
                    echo "Build completed successfully" > build/build-info.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    test -f build/Jenkinsfile
                    echo "Tests passed successfully"
                '''
            }
        }

        stage('Package Application') {
            steps {
                sh '''
                    tar -czf application.tar.gz build
                    echo "Application packaged successfully"
                '''
            }
        }

        stage('Deliver Artifact') {
            steps {
                archiveArtifacts artifacts: 'application.tar.gz', fingerprint: true
            }
        }
    }
}
