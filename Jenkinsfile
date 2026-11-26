pipeline {
    agent any

    environment {
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
    }

    stages {
        stage('Verification') {
            steps {
                sh 'test -f app.py && test -f Dockerfile'
            }
        }

        stage('Build Docker') {
            steps {
                sh 'docker build -t mon-app-devops:v1 .'
            }
        }

        stage('Deploiement Kubernetes') {
            steps {
                sh 'sudo -u vagrant /usr/local/bin/minikube image load mon-app-devops:v1'
                sh 'KUBECONFIG=/home/vagrant/.kube/config kubectl apply -f deployment.yaml'
                sh 'KUBECONFIG=/home/vagrant/.kube/config kubectl apply -f service.yaml'
            }
        }
    }
}
