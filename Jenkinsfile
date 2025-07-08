pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/naveenleon/k8s-projecty.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t gamepro /var/lib/jenkins/workspace/k8s-project'
                sh 'sudo docker tag gamepro naveenleon/gamepro:latest'
                sh 'sudo docker tag gamepro naveenleon/gamepro:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push naveenleon/gamepro:latest'
                sh 'sudo docker image push naveenleon/gamepro:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/k8s-projecty/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
