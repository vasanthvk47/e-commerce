pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/vasanthvk47/e-commerce.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("e-commerce")
                }
            }
        }

        stage('Push to DockerHub') {
    steps {
        script {
            docker.withRegistry('', 'dockerhub-password') {
                sh 'docker tag e-commerce vasanth4747/e-commerce:latest'
                sh 'docker push vasanth4747/e-commerce:latest'
            }
        }
    }
}


        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
