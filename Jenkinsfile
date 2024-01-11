pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Suriya-Vijayan/kubernetes-Python.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t imagev1 /var/lib/jenkins/workspace/DEMO-K8S'
                sh 'sudo docker tag imagev1 suriyavijayan1126/newimage:latest'
                sh 'sudo docker tag imagev1 suriyavijayan1126/newimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push suriyavijayan1126/imagev1:latest'
                sh 'sudo docker image push suriyavijayan1126/imagev1:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/DEMO-K8S/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
