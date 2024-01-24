pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    // Assuming Dockerfile is in the root of your project
                    sh "docker build -t docker-image:latest ."
                }
                script {
                    // Run the container in detached mode, and publish port 8057
                    sh "docker run -d -p 8057:80 --name my-container docker-image:latest"
                }
            }
        }

        stage('Testing Container') {
            steps {
                script {
                    // Wait for the container to be ready (adjust sleep time based on your application startup time)
                    sh 'sleep 20'

                    // Use localhost since Jenkins and the Docker container are likely on the same machine
                    sh "curl http://10.196.153.137:8057"
                }
            }
        }
    }

    post {
        always {
            // Stop and remove the container after testing
            script {
                sh "docker stop my-container || true"
                sh "docker rm my-container || true"
            }
        }
    }
}
