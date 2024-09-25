pipeline {
    agent any
    environment {
        // Using environment variables to store credentials securely
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Building the Docker image and tagging it with the build ID
                    docker.build("abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID}")
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    // Logging into Docker Hub and pushing the image
                    docker.withRegistry('https://index.docker.io/v1/', 'DOCKERHUB_CREDENTIALS') {
                        docker.image("abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID}").push()
                    }
                }
            }
        }
    }
    post {
        always {
            // Cleaning up the Docker images to save space on the Jenkins server
            echo 'Cleaning up...'
            sh "docker rmi abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID}"
        }
    }
}
