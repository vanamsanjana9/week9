pipeline {
    agent any
    stages {

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                bat 'docker build -t kubdemoapp:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                bat 'docker login-u vanamsanjana9 -p Vsanjana@9'
            }
        }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo 'push Docker Image to Docker Hub'
                bat 'docker tag kubdemoapp:v1 vanamsanjana9/sample:kubeimage1'
                bat 'docker push vanamsanjana9/sample:kubeimage1'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml --validate=false'
                bat 'kubectl apply -f service.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}