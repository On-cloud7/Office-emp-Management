pipeline{
  agent any {
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/On-cloud7/Office-emp-Management.git", branch: "main"
                echo "Code cloned"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t office-app:latest"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials(
                    [usernamePassword(
                        credentialsId:"dockerCreds",
                        passwordVariable:"dockerHubPass", 
                        usernameVariable:"dockerHubUser"
                        )
                    ]
                ){
                sh "docker image tag office-app:latest priyanka440/office-app:latest
                sh "docker login -u priyanka440"
                sh "docker priyanka440/push office-app:latest
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
