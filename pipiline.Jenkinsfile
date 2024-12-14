pipeline {
    agent any

    stages {
        stage('List Pods') {
            steps {
                script {
                    echo "Listando os Pods no Cluster Kubernetes"
                    // Lista os pods no namespace padrão
                    sh 'kubectl get pods'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline executada com sucesso."
        }
        failure {
            echo "Falha na execução. Verifique os logs."
        }
    }
}
