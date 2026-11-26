pipeline {
    agent any

    environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
    }

    stages {
        stage('Verification') {
            steps {
                sh 'test -f app.py'
                sh 'test -f Dockerfile'
            }
        }

        stage('Build Docker') {
            steps {
                sh 'docker build -t mon-app-devops:v1 .'
            }
        }

        stage('Deploiement Kubernetes') {
            steps {
                sh 'minikube image load mon-app-devops:v1'
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
