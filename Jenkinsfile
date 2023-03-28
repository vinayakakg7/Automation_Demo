pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/vinayakakg7/Automation_Demo.git'
      }
    }
    stage('Terraform Script Run') {
      steps {
          // Initialize the Terraform working directory
          bat 'terraform init'
          bat 'terraform plan'
          bat 'terraform ${'terra'} --auto-approve'
         // bat 'terraform apply --auto-approve'
         // bat 'terraform destroy --auto-approve'
        }
      }
      }
    }
