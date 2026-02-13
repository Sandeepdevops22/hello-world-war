pipeline {
    agent any

    environment {
        IMAGE_NAME = "sandeep2210/hello-world-war-image"
        IMAGE_TAG = "latest"
        DOCKER_CREDS = credentials('dockerhub-creds')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sandeepdevops22/hello-world-war.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('DockerHub Login') {
            steps {
                sh """
                echo ${DOCKER_CREDS_PSW} | docker login -u ${DOCKER_CREDS_USR} --password-stdin
                """
            }
        }

        stage('Push Image') {
            steps {
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }

        stage('Deploy to Tomcat Container') {
            steps {
                sh """
                docker stop hello-app || true
                docker rm hello-app || true
                docker run -d -p 8080:8080 --name hello-app ${IMAGE_NAME}:${IMAGE_TAG}
                """
            }
        }
    }
}

