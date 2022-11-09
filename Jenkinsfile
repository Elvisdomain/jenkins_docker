pipeline {
    agent any
    environment {
        DOCKER_TAG = getDockerTag()
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build . -t elvisdomain/nodeapp:${DOCKER_TAG} "
            }
        }
        stage('DockerHub Push') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                    sh "docker login -u elvisdomain -p ${dockerHubPwd}"
                    sh "docker push elvisdomain/nodeapp ${DOCKER_TAG}:latest"
                }
            }
        }
    }
}

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}