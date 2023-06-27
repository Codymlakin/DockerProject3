pipeline {
    agent any

    stages {
        stage('Build Docker image') {
            steps {
                sh 'docker build -t cmlakin/eaglesproject3 .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                    sh 'aws eks update-kubeconfig --name EaglesCluster'
                    sh 'kubectl get nodes'
                    sh 'kubectl apply -f eagles-deployment.yaml'
                    sh 'kubectl apply -f eagles-service.yaml'
                    
                }
            }
        }
    }