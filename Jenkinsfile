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
        }
      }
      stage('Terraform action') {
        steps {
            echo 'terraform action --> ${terra}'
             if (isUnix()) {
                sh "terraform ${terra} --auto-approve"
                 } else {
                     bat "terraform ${terra} --auto-approve"
    }
  }
}

      }
    }
