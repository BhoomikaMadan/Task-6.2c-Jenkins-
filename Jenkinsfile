pipeline {
    agent any
    environment {
        EMAIL = 'your_email@example.com' // Change to your email
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean package' // Example for Java/Maven build
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'  // Example for running tests
            }
            post {
                success {
                    emailext (
                        subject: "Unit Tests Passed",
                        body: "Unit tests completed successfully.",
                        to: "${EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Unit Tests Failed",
                        body: "Unit tests failed. Check Jenkins logs.",
                        to: "${EMAIL}"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                sh 'sonar-scanner'  // Example for SonarQube
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'npm audit'  // Example for Node.js security check
            }
            post {
                success {
                    emailext (
                        subject: "Security Scan Passed",
                        body: "Security scan completed successfully.",
                        to: "${EMAIL}"
                    )
                }
                failure {
                    emailext (
                        subject: "Security Scan Failed",
                        body: "Security vulnerabilities found. Check Jenkins logs.",
                        to: "${EMAIL}"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                sh './deploy-to-staging.sh' // Write this script for AWS EC2 deployment
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh './run-staging-tests.sh'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                sh './deploy-to-production.sh'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
