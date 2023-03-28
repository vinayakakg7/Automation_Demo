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

    stage('Terraform Plan') {
    withCredentials([<object of type com.cloudbees.jenkins.plugins.awscredentials.AmazonWebServicesCredentialsBinding>]) {
      steps {
        bat 'terraform plan'
      }
    }

    }

    stage('Terraform Apply') {
      steps {
        bat 'terraform apply --auto-approve'
      }
    }
  }
}
