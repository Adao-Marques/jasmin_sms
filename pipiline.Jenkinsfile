pipeline {
    agent any
    environment {
        KUBECONFIG = 'kubeconfig.txt' // Caminho para o arquivo kubeconfig
    }
    stages {
        stage('Preparar') {
            steps {
                echo 'Verificando a configuração do kubectl'
                sh 'kubectl version --client' // Confirma que o kubectl está instalado e funcional
            }
        }
        stage('Aplicar YAMLs') {
            steps {
                script {
                    echo 'Aplicando arquivos YAML no Kubernetes'
                    sh '''
                        kubectl apply -f k8s-yaml-files/redis.yml
                        kubectl apply -f k8s-yaml-files/rabbitmq.yml
                        kubectl apply -f k8s-yaml-files/jasmin.yml 
                        kubectl apply -f k8s-yaml-files/observability.yml
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Arquivos YAML aplicados com sucesso!'
        }
        failure {
            echo 'Erro ao aplicar os arquivos YAML. Verifique os logs.'
        }
    }
}
