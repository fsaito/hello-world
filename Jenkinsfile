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
                    sh "sudo docker push iad.ocir.io/idreywyoj0pu/fsaito/hello-world:latest"
            }
        }
        stage('Deploy to k8s'){
            steps{
                sh "sudo /usr/local/bin/kubectl create -f manifest.yml"

                        
            }
        }  
    }
}
