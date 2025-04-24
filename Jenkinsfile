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
                    junit 'junit.xml'  /
                }
            }
        }

        stage('Run Website') {
            steps {
                sh 'npm start & sleep 10' // run in background for testing
                echo 'Website is running (simulated)'
            }
        }
    }
}
