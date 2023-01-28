pipeline {
    agent any

    stages {

        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("leofarias/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage ('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com','dockerhub')
                        dockerapp.push('latest')
                        dockerapp.pus("${env.BUILD_ID}")
                }
            }
        }
    }
}