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
                    sh 'kubectl get nodes'
                    // sh 'kubectl apply -f your-kubernetes-manifests.yaml'
                    // Replace 'your-kubeconfig-credentials' with the ID of your Kubernetes configuration credentials in Jenkins
                    // Replace 'your-kubernetes-manifests.yaml' with the path to your Kubernetes manifests file
                }
            }
        }
    }