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
                git url: "https://github.com/rajatrokde/Python-app.git", branch: "dev" 
            }
        }

        stage("Build") {
            steps {
                echo "Building the image"
                 bat "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId: "DockerHubcred", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                     bat "docker login -u ${dockerHubUser} -p ${dockerHubPass}"
                     bat "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${dockerHubUser}/${IMAGE_NAME}:${IMAGE_TAG}"
                    bat "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the container"
               

                bat "docker-compose down && docker-compose pull && docker-compose up -d"
            }
        }
    }
}
