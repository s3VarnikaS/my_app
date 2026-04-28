pipeline {
    agent any
    environment {
        IMAGE_NAME = "varnikas01/myapp"
    }
    stages {
        stage('Clone Source') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/s3VarnikaS/my_app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    sh '''
                    echo $DOCKER_TOKEN | docker login -u varnikas01 --password-stdin
                    '''
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }
}
