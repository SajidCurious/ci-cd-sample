pipeline {
    agent any
    environment {
        IMAGE_NAME = 'sajidcurious/ci-cd-sample'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    // Docker login (using Jenkins environment variables)
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'

                    // Push the Docker image to Docker Hub
                    docker.image("${IMAGE_NAME}:latest").push()
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
