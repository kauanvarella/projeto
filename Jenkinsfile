pipeline {
    agent { dockerfile true }
    stages {       
        stage('Provisionando Infraestrutura') {
            steps {
                withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'terraform-aws', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    echo 'DESTRUINDO INSTANCIA - DESTRUINDO INSTANCIA - DESTRUINDO INSTANCIA - DESTRUINDO INSTANCIA - DESTRUINDO INSTANCIA - DESTRUINDO INSTANCIA - DESTRUINDO INSTANCIA'
                    sh 'terraform destroy -target aws_instance.app_server -auto-approve'
                    echo 'INICIANDO TERRAFORM - INICIANDO TERRAFORM - INICIANDO TERRAFORM - INICIANDO TERRAFORM - INICIANDO TERRAFORM  - INICIANDO TERRAFORM  - INICIANDO TERRAFORM '
                    sh 'terraform init'
                    echo 'APLICANDO TERRAFORM - APLICANDO TERRAFORM - APLICANDO TERRAFORM - APLICANDO TERRAFORM - APLICANDO TERRAFORM - APLICANDO TERRAFORM - APLICANDO TERRAFORM'
                    sh 'terraform apply -auto-approve'
                }  
            }
        }
        stage('Configurando a instancia com Ansible') {
            steps {
                sh 'sleep 10'
                sh 'chmod 600 ssh-prod-meuapp.pem'
                ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts.inv', playbook: 'playbook.yml'
            }
        }
    }
}