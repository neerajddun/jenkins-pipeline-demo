pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("my-jenkins-demo")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    dockerImage.run('-d --name demo-container')
                    echo 'Container started successfully!'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker rm -f demo-container || true'
        }
    }
}
