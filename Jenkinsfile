pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "sudo docker build . -t fsaito/hello-world"
            }
        }
        stage('DockerHub Push'){
            steps{
                    sh "sudo docker tag fsaito/hello-world iad.ocir.io/idreywyoj0pu/fsaito/hello-world:latest"
                    sh "sudo docker push iad.ocir.io/idreywyoj0pu/fsaito/hello-world:latest"
            }
        }
        stage('Deploy to k8s'){
            steps{
                sh "sudo /usr/local/bin/kubectl run hello-world-jenkins --image=iad.ocir.io/idreywyoj0pu/fsaito/hello-world:latest --port 8000 --expose"
                sh "sudo /usr/local/bin/kubectl expose deployment hello-world-jenkins  --type=LoadBalancer --name=hello-world-jenkins-lb"

                        
            }
        }  
    }
}


def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
