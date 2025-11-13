pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    dockerImage = docker.build("my-jenkins-demo")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Run the container in detached mode
                    def container = dockerImage.run('-d --name demo-container')
                    echo "Container started successfully!"
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Stop and remove container if exists
            sh 'docker rm -f demo-container || true'
        }
    }
}
