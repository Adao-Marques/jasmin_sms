pipeline {
    agent any

    environment {
        MINIKUBE_STATUS = "UNKNOWN"
    }

    stages {
        stage('Check Minikube Status') {
            steps {
                script {
                    // Verifica o status do Minikube
                    MINIKUBE_STATUS = sh(
                        script: "minikube status --format '{{.Host}}'",
                        returnStdout: true
                    ).trim()
                    
                    echo "Minikube status: ${MINIKUBE_STATUS}"
                }
            }
        }

        stage('Start Minikube (if stopped)') {
            when {
                expression { MINIKUBE_STATUS == 'Stopped' }
            }
            steps {
                echo 'Minikube is stopped. Starting the cluster...'
                sh 'minikube start --driver=docker'  // Aqui você pode usar o driver necessário
            }
        }

        stage('Cluster Verification') {
            steps {
                script {
                    def kubeNodes = sh(
                        script: "kubectl get nodes --no-headers | wc -l",
                        returnStdout: true
                    ).trim()
                    
                    if (kubeNodes.toInteger() > 0) {
                        echo "Cluster is running with ${kubeNodes} node(s)."
                    } else {
                        error "Failed to start the Minikube cluster."
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed."
        }
        success {
            echo "Cluster is up and running!"
        }
        failure {
            echo "Something went wrong. Check the logs."
        }
    }
}
