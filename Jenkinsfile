pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Checkout the code from your repository
                git url: 'https://github.com/torresJ04/pedelogo-catalogo', branch: 'main'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    // Build the Docker image using the specified Dockerfile
                    def dockerApp = docker.build("fabricioveronez/api-produto:${env.BUILD_ID}", '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    // Push the built image to Docker Hub using the credentials identified by 'dockerhub'
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerApp.push("${env.BUILD_ID}")
                        dockerApp.push("latest")
                    }
                }
            }
        }
    }
}