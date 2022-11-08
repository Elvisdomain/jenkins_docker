pipeline {
    agent any
    environment {
        DOCKER_TAG = getDockerTag()
    }
    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build . -t elvisdomain/nodeapp:${DOCKER_TAG}"
            }
        }
        stage('DockerHub Push') {
            sh "docker login -u elvisdomain -p"
        }
    }
}

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}