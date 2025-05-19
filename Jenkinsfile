pipeline {
    agent any 
    environment {
        IMAGE_NAME = "rajatrokde9/python-app" // Replace with your actual DockerHub repo name
        IMAGE_TAG = "v2"
    }
   stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/rajatrokde/Python-app.git", branch: "main"
            }
        
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
        
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                    withCredentials([usernamePassword(credentialsId: "DockerHubcred", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                    sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${env.dockerHubUser}:${IMAGE_TAG} "
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                    
                }
            }
    }
    
}
}
