pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "clonning the code"
                git url: "https://github.com/lokeshj2403/discovery.git", branch: "main"
            }
        }
        stage("Build"){
            steps{
                echo "building the code"
                sh "docker build -t demo ."
            }
        }
        stage("DockerPush"){
            steps{
                echo "pushing image to Docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"Loki@1234",usernameVariable:"lokeshj2403")]){
                sh "docker tag tendergarden ${env.lokeshj2403}/demo:latest"
                sh "docker login -u ${env.lokeshj2403} -p ${env.Loki@1234}"
                sh "docker push ${env.lokeshj2403}/demo:latest"
                }
            }
        }
        stage("deploy"){
            steps{
                echo "deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
