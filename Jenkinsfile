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
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-credentials') {
                        docker.image("${IMAGE_NAME}").push()
                    }
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
