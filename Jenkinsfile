pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/vinayakakg7/Automation_Demo.git'
      }
    }
    stage('Terraform Plan') {

      environment {
        // Initialize the AWS access key and secret key variables as empty strings
        AWS_ACCESS_KEY = ""
        AWS_SECRET_KEY = ""
      }
      steps {
        // Retrieve the AWS access key and secret key from the Jenkins credentials store
        withCredentials([usernamePassword(credentialsId: 'aws_cred', passwordVariable: 'AWS_SECRET_KEY', usernameVariable: 'AWS_ACCESS_KEY')]) {
          // Initialize the Terraform working directory
          bat 'terraform init'
          // Generate a Terraform plan with the AWS access key and secret key as variables
          bat 'terraform plan -var "aws_access_key=$AWS_ACCESS_KEY" -var "aws_secret_key=$AWS_SECRET_KEY"'
        }
      }
      }
    }
  }
