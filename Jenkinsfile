pipeline {
    agent any 
    stages{
        stage("code"){
            steps{
                echo "cloning the code"
                git url:"https://github.com/shadab-ahmed23/django-notes-app.git",branch:"main"
            }
        }
        stage("build"){
            steps{
                echo "building the code"
                sh "docker build -t my-note-app ."
            }
        }
        stage("pushing image"){
            steps{
                echo "push the image"
                 withCredentials([usernamePassword(credentialsId:"DockerHub-ID",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker tag my-note-app shadabahmed23/my-note-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                     sh "docker push shadabahmed23/my-note-app:latest"
                
            
            }
            }
        }
        stage("deploye image"){
            steps{
                echo "deploye the image"
                sh "docker-compose down && docker-compose up -d"
            
            }
            
        }
    }
}
