@Library("shared") _
pipeline{
    agent { label 'bk'}
    
    stages{
        stage("Code clone"){
            steps{
                sh "whoami"
            clone("https://github.com/bhavesh-kumawat/two-tier-flask-app.git","master")
            }
        }
        stage("Code Build"){
            steps{
            docker_build("two-tier-backend","latest")
            }
        }
        stage("Tag image"){
            steps{
            tag_docker_image("two-tier-backend","latest","DockerHubCred")
            }
        }
        stage("Push to DockerHub"){
            steps{
                docker_push("two-tier-backend", "latest", "DockerHubCred")
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying th code"
                sh "docker compose up -d"
            }
        }

    }
}
