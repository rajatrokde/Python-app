pipeline {
    agent any 

    environment {
        IMAGE_NAME = "rajatrokde9/python-app"
        IMAGE_TAG = "v2dev"
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

        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId: "DockerHubcred", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                    sh "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                    sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${dockerHubUser}/${IMAGE_NAME.split('/')[1]}:${IMAGE_TAG}"
                    sh "docker push ${dockerHubUser}/${IMAGE_NAME}:${IMAGE_TAG}"
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
