pipeline {
    agent any

    stages {
        stage('Code') {
            steps {
                echo 'Cloning the code from GitHub' 
                git url:"https://github.com/shadab-ahmed23/django-notes-app.git",branch:"main"
            }
        }
        stage('Build') {
            steps {
                echo 'Building the code from '
                sh "docker build -t my-note-app ."
            }
        }
        stage('push to dockerHub') {
            steps {
                echo 'push the image to dockerHub'
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker tag my-note-app shadabahmed23/my-note-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                     sh "docker push shadabahmed23/my-note-app:latest"
                }
            }
        }
        stage('Dploy') {
            steps {
                echo 'Deploying the code'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

