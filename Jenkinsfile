pipeline {
    agent {
        docker {
            image 'node:18-alpine'
        }
    }

    environment {
        CI = 'true'
    }

    stages {
        stage('Clone Project') {
            steps {
                git url: 'https://github.com/BS-PM-2025/BS-PM-2025-TEAM24.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'npm test -- --ci --reporters=jest-junit'
            }
            post {
                always {
                    junit 'junit.xml'
                }
            }
        }

        stage('Run Website') {
            steps {
                sh 'npm start & sleep 10'
                echo 'Website is running (simulated)'
            }
        }
    }
}
