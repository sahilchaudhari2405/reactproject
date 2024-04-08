pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'my-node-app'
        DOCKERFILE_PATH = './Dockerfile'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build("${DOCKER_IMAGE_NAME}", "-f ${DOCKERFILE_PATH} .")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container based on the built image
                    docker.image("${DOCKER_IMAGE_NAME}").run('-p 8080:80 --name my-container -d')
                }
            }
        }
    }

    post {
        success {
            echo 'Docker container started successfully.'
        }
        failure {
            echo 'Failed to start Docker container.'
        }
    }
}
