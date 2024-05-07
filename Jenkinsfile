pipeline {
    agent any
    
    stages{
        stage('Clone Code'){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/GOPALGTM/node-todo-app.git", branch:"main"
            }
        }
        stage('Build'){
            steps {
                echo "Building the Image -"
                sh "sudo docker build -t todo-app ."
            }
        }
        stage('push to dockerhub'){
            steps {
                echo "Pushing the code to dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "sudo docker tag todo-app ${env.dockerHubUser}/node-app:latest"
                sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "sudo docker push ${env.dockerHubUser}/node-app:latest"
                }
            }
        }
        stage('Deploy'){
            steps {
                echo "Deploying the application"
                sh "sudo docker-compose down"
                sh "sudo docker-compose up -d --build"
                
            }
        }
    }
}
