@Library("Shared") _
pipeline{
    
    agent { label 'lucky'}
    
    stages{
        
        stage("Code"){
            steps{
                script{
                    clone("https://github.com/lokeshsolanki12/Django-Projecs-Jenkins.git", "main")
                }
            }
        }
        stage("Build"){
            steps{
                script{
                    docker_build("notes-app", "latest", "lokeshsolanki12")
                }
            }
        }
        stage("Push on DockerHub") {
            steps {
                script {
                    docker_push(
                        credentialsId: 'dockerHubCred',
                        imageName: 'notes-app',
                        imageTag: 'latest'
                        )
                    }
                }
            }
        stage("Deploy"){
            steps{
                sh "docker compose down && docker compuse up -d"
            }
        }
    }
}
