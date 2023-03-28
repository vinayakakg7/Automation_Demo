pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/vinayakakg7/Automation_Demo.git'
      }
    }

    stage('Terraform Init') {
      steps {
        bat 'terraform init'
      }
    }

    stage('Terraform Apply') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'aws_cred', passwordVariable: 'AWS_SECRET_KEY', usernameVariable: 'AWS_ACCESS_KEY')]) {
                    bat 'terraform plan'
                    bat 'terraform apply --auto-approve'
            }
        }
    }
  }
}
