pipeline {
    agent any 

    environment {
        IMAGE_NAME = "rajatrokde/python-app" // Replace with your actual DockerHub repo name
        IMAGE_TAG = "v1"
    }

    stages {
        stage("Clone Code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/rajatrokde/Python-app.git", branch: "main"
            }
        }

        stage("Build") {
            steps {
                echo "Building the Docker image"
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the container"
                sh "docker-compose down || true"
                sh "docker-compose up -d"
            }
        }

        stage("Push to Docker Hub") {
            steps {
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(
                    credentialsId: "dockerHub", 
                    usernameVariable: "dockerHubUser", 
                    passwordVariable: "dockerHubPass"
                )]) {
                    sh """
                        docker login -u $dockerHubUser -p $dockerHubPass
                        docker tag ${IMAGE_NAME}:${IMAGE_TAG} $dockerHubUser/python-app:${IMAGE_TAG}
                        docker push $dockerHubUser/python-app:${IMAGE_TAG}
                    """
                }
            }
        }
    }
}
