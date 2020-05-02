pipeline{
    agent any
    environment{
         DOCKER_TAG = getDockerTag()
    }
    stages{
        stage("Build docker image"){
            steps{
                sh "docker build . -t sathishkumarpkd/node-app:${DOCKER_TAG}"
            }
        }
         stage("Push docker image"){
            steps{
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerhubpwd')]) {
                     sh "docker login -u sathishkumarpkd -p ${dockerhubpwd}"
                     sh "docker push sathishkumarpkd/node-app:${DOCKER_TAG}"
                }
            }
        }
    }
}

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
