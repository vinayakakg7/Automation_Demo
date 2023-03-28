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
            bat "terraform ${terra} --auto-approve"
    }
  }
  stage('Build and test using Maven') {
            steps {
                bat 'mvn clean install -DskipTests=true'
            }
        }
     stage("deploy-dev"){
        steps{
             script {
                def public_ip = sh(returnStdout: true, script: 'terraform output public_ip').trim()
                sshagent(['Deploy_Auto']) {
              //public_ip= $(terraform output public_ip)
				bat  "scp -o StrictHostKeyChecking=no C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Automation_Demo\\target\\springbootApp.jar ec2-user@public_ip: /usr/local/tomcat9/webapps/ "
				bat  "ssh -o StrictHostKeyChecking=no ec2-user@public_ip tomcatdown"
				bat  "ssh -o StrictHostKeyChecking=no ec2-user@public_ip tomcatup" 

          
					}
				}
			}  
     }
}
}
    
