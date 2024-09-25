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
                    // Explicitly tag and build the Docker image
                    sh "docker build -t abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID} ."
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    // Logging into Docker Hub and pushing the image
                    docker.withRegistry('https://index.docker.io/v1/', 'DOCKERHUB_CREDENTIALS') {
                        sh "docker push abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID}"
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
