pipeline {
    agent any
    environment {
        IMAGE_NAME = "pradhisha/java-helloworld:latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url:'https://github.com/Pradhisha-N/java-helloworld.git',branch:'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
        stage('Scale Deployment') {
            steps {
                sh 'kubectl scale deployment helloworld-deployment --replicas=3'
            }
        }
    }
}
