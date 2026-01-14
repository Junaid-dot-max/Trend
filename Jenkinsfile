pipeline {
    agent any

    environment {
        IMAGE_NAME = "ahamedjunaid/trend-nginx"
        IMAGE_TAG  = "latest"
        KUBECONFIG = "/var/snap/jenkins/common/.kube/config"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t trend-nginx .
                '''
            }
        }

        stage('Tag & Push Image to DockerHub') {
            steps {
                sh '''
                docker tag trend-nginx ${IMAGE_NAME}:${IMAGE_TAG}
                docker push ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }

        stage('Deploy to Kubernetes (EKS)') {
            steps {
                sh '''
                kubectl apply -f deployment.yaml
                kubectl apply -f service.yaml
                '''
            }
        }
    }

    post {
        success {
            echo "✅ CI/CD Pipeline completed successfully"
        }
        failure {
            echo "❌ CI/CD Pipeline failed"
        }
    }
}
