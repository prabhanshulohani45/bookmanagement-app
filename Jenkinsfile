pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "prabhanshulohani45/bookmanagement-app"
        DOCKER_TAG = "latest"
    }

    stages {
        stage('Clone Repository'){
            steps {
                git branch: 'main', url:'https://github.com/prabhanshulohani45/bookmanagement-app.git'
            }
        }

        stage('Build Maven Project'){
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image'){
            steps {
                sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId:'docker-hub-credentials',url:'']){
                    sh 'docker push ${DOCKER_IMAGE}:${DOCKER_TAG}'
                }
            }
        }
        
        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8082:8081 --name bookmanagement-app-container ${DOCKER_IMAGE}:${DOCKER_TAG}'
            }
        }
       
    }

}
