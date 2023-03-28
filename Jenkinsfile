pipeline {
  agent any
  environment {
  AWS_ACCESS_KEY = "${credentials('aws_cred').username}"
  AWS_SECRET_ACCESS_KEY = "${credentials('aws_cred').password}"
}

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/vinayakakg7/Automation_Demo.git'
      }
    }
    stage('Terraform Plan') {
      steps {
        bat 'terraform init'
        bat 'terraform plan -var "aws_access_key=${AWS_ACCESS_KEY}" -var "aws_secret_key=${AWS_SECRET_KEY}"'
		bat 'terraform apply --auto-approve -var "aws_access_key=${AWS_ACCESS_KEY}" -var "aws_secret_key=${AWS_SECRET_KEY}"'
      }
    }
  }
}
