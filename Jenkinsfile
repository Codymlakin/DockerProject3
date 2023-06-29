pipeline {
    agent any

    stages {
        stage('Restart Deployment') {
            steps {
                script {
                    withAWS(credentials: 'aws_creds') {
                        sh 'aws eks update-kubeconfig --name EaglesCluster'
                    }
                }
            }
        }

        stage('Build Docker image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'jenkins', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                        sh 'docker build -t cmlakin/eaglesproject3 .'
                        sh 'docker push cmlakin/eaglesproject3'
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withAWS(credentials: 'aws_creds') {
                        sh 'aws eks update-kubeconfig --name EaglesCluster'
                        sh 'kubectl get nodes'
                        sh 'kubectl apply -f deployment.yaml'
                        sh 'kubectl apply -f service.yaml'
                        sh 'kubectl get service eagles-service'
                        sh 'kubectl rollout restart deployment eagles-deployment'
                    }
                }
            }
        }
    }
}



