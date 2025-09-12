pipeline {
    agent any
    tools {
        nodejs "node18"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/janki10-l/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
            post {
                success {
                    emailext (
                        subject: "SUCCESS: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                        body: "Build succeeded!\n\nCheck details at: ${env.BUILD_URL}",
                        to: "jankiluitel10@gmail.com"
                    )
                }
                failure {
                    emailext (
                        subject: "FAILURE: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                        body: "Build failed!\n\nCheck logs at: ${env.BUILD_URL}",
                        to: "jankiluitel10@gmail.com"
                    )
                }
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
            post {
                success {
                    emailext (
                        subject: "SECURITY SCAN PASSED: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                        body: "Security scan passed!\n\nCheck details at: ${env.BUILD_URL}",
                        to: "jankiluitel10@gmail.com"
                    )
                }
                failure {
                    emailext (
                        subject: "SECURITY SCAN FAILED: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                        body: "Security scan found issues!\n\nCheck logs at: ${env.BUILD_URL}",
                        to: "jankiluitel10@gmail.com"
                    )
                }
            }
        }
    }
}

