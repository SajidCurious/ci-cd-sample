pipeline {
    agent any
    environment {
        // Define your Docker image name and tag (make sure it's correct)
        IMAGE_NAME = 'sajidcurious/ci-cd-sample:latest'  // Use the correct username and repository name
    }
    stages {
        stage('Build') {
            steps {
                script {
                    // Build the Docker image
                    docker.build("${IMAGE_NAME}")
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    // Docker login with credentials from Jenkins
                    echo "Logging in to Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-cred') {
                        // Push the Docker image to Docker Hub
                        echo "Pushing the image to Docker Hub..."
                        docker.image("${IMAGE_NAME}").push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Deploy your app to Kubernetes (if applicable)
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
