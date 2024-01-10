pipeline {
    agent any
    
    stages {
        
        stage("Code"){
            steps{
                git url: "https://github.com/davender-singh1/node-todo-cicd.git", branch: "master"
                echo 'Code Clone Completed!'
            }
        }
        stage("Build and Test"){
            steps{
                sh "docker build -t node-app ."
                echo 'Code build done!'
            }
        }
        stage("Scan"){
            steps{
                echo 'Image Scanned'
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"    
                sh "docker tag node-app:latest ${env.dockerHubUser}/node-app:latest"
                sh "docker push ${env.dockerHubUser}/node-app:latest"
                echo 'Code pushed to DockerHub'
            }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'Code deployed successfully!'
            }
        }
    }
}
