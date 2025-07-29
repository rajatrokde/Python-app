pipeline {
    agent any

    environment {
        IMAGE_NAME = "rajatrokde9/python-app"
        IMAGE_TAG = "latest"
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
                echo "Building the image"
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId: "DockerHubcred", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                    sh "echo ${dockerHubPass} | docker login -u ${dockerHubUser} --password-stdin"
                    // Make sure to use fully qualified image name for push
                    sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose pull && docker-compose up -d"
            }
        }
    }
}
