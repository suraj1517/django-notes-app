pipeline {
    agent any 
     environment {
        DockerHub = credentials('dockerHub')
    }
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/suraj1517/django-notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
                stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")])
                {
                     sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                     sh("curl -u ${dockerHubUser}:${dockerHubPass} https://hub.docker.com/")
                     sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
    }
}
