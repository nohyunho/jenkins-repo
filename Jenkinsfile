pipeline {
  agent {
    node {
      label 'jenkins-jenkins-slave'
    }

  }
  stages {
    stage('Set Terraform Env') {
      steps {
        script {
          def tfHome = tool name: 'terraform-0.12.29'
          env.PATH = "${tfHome}:${env.PATH}"
        }

        withVault(configuration: [vaultUrl: 'https://dodt-vault.acldevsre.de',  vaultCredentialId: 'approle-for-vault', engineVersion: 2], vaultSecrets: [[path: 'jenkins/jmungmoong.roh/acl-dev-credentials', secretValues: [[envVar: 'AWS_ACCESS_KEY_ID', vaultKey: 'accessKey'], [envVar: 'AWS_SECRET_ACCESS_KEY', vaultKey: 'secretKey']]]]) {
          sh 'terraform version'
        }

      }
    }

    stage('Terraform init') {
      steps {
        sh '''sleep 1000
cd terraform/
terraform init'''
      }
    }

    stage('Terraform plan') {
      steps {
        sh '''cd terraform/
terraform plan'''
      }
    }

    stage('Deploy Approval') {
      steps {
        input(message: 'Are you Confirm?', submitter: 'admin')
      }
    }

    stage('Terraform apply') {
      steps {
        sh '''cd terraform/
terraform apply -auto-approve'''
      }
    }

  }
}