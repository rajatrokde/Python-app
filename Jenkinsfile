pipeline {
    agent any 
    
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
                sh "docker build -t DOCKER_REPO ." 
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
                    withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerHubPass", usernameVariable: "dockerHubUser")]) {
                    sh "docker tag demoportfolio ${env.dockerHubUser}/DOCKER_REPO:v1"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/DOCKER_REPO:v1"
                    
                }
            }
    }
    
}
}
