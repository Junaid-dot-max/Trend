pipeline {
  agent any

  environment {
    IMAGE = "ahamedjunaid/trend-nginx:latest"
    KUBECONFIG = "/var/snap/jenkins/common/.kube/config"
  }

  stages {

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t trend-nginx .'
      }
    }

    stage('Push Image to DockerHub') {
      steps {
        sh '''
          docker tag trend-nginx $IMAGE
          docker push $IMAGE
        '''
      }
    }

    stage('Deploy to EKS') {
      steps {
        sh '''
          kubectl apply -f deployment.yaml
          kubectl apply -f service.yaml
        '''
      }
    }
  }
}
