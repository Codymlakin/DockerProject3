  agent any
  stages {
    stage('Example') {
      steps {
        withAWS(credentials: 'AKIA3NT52SLXJIHOZ47Z') {

          // Your AWS-related steps or commands here

        }
      }
    }
  }
}


pipeline {
    agent any

    stages {
        stage('Restart Deployment') {
            steps {
                sh 'aws eks update-kubeconfig --name EaglesCluster'
                
            }
        }

        stage('Build Docker image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'jenkins', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        sh 'docker build -t cmlakin/eaglesproject3 .'
                        sh 'docker push cmlakin/eaglesproject3'
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl get nodes'
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
                sh 'kubectl get service eagles-service'
                sh 'kubectl rollout restart deployment eagles-deployment'
            }
        }
    }
}

