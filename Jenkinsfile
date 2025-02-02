pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git url: '', branch: 'main'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    docker app = docker.build("fabricioveronez/api-produto: ${env.BUILD_ID}",
                    '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push("${env.BUILD_ID}")
                        dockerapp.push("latest")
                    }
                }
            }
        }
    }
}