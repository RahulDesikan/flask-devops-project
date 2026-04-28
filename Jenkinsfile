pipeline {
    agent any

    environment {
        DOCKER_HUB = "rahuldesikan"
        IMAGE_NAME = "flask-app"
    }

    stages {

        stage('Clone') {
            steps {
                echo 'Using source from GitHub'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Tag Image') {
            steps {
                sh 'docker tag $IMAGE_NAME $DOCKER_HUB/$IMAGE_NAME:latest'
            }
        }

        stage('Login DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $DOCKER_HUB/$IMAGE_NAME:latest'
            }
        }
    }
}