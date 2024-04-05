pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/vijay3639/k8s-project.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t new1image /var/lib/jenkins/workspace/k8s-project'
                sh 'sudo docker tag new1image vijay3639/new1image:latest'
                sh 'sudo docker tag new1image vijay3639/new1image:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push vijay3639/new1image:latest'
                sh 'sudo docker image push vijay3639/new1image:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/k8s-project/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
