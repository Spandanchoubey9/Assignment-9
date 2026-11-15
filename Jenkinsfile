
pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\Users\\spand\\.kube\\config'
        TRIVY = 'C:\\Users\\spand\\AppData\\Local\\Microsoft\\WinGet\\Packages\\AquaSecurity.Trivy_Microsoft.Winget.Source_8wekyb3d8bbwe\\trivy.exe'
    }

    stages {
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t assignment-9-app .'
            }
        }

        stage('Security Scan') {
            steps {
                bat '"%TRIVY%" image --exit-code 0 --severity HIGH,CRITICAL assignment-9-app'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl rollout status deployment/healthcare-app'
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }
}
