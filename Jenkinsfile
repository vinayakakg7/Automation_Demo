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
        script {
      // Get the value of the "terra" parameter
            def terra = params.terra

      // Check if the "terra" parameter is set to "destroy"
                if (terra == 'destroy') {
                      echo 'Destroying infrastructure...'
                      bat "terraform destroy --auto-approve"
                      error "Aborting the pipeline after destroying infrastructure" // Stop the pipeline after the destroy command
                    } else {
                          echo 'Applying infrastructure...'
                          bat "terraform apply --auto-approve"
                        }
                      }
                    }
                  }
    stage('Build and test using Maven') {
            steps {
                bat 'mvn clean install -DskipTests=true'
            }
        }
//    stage("deploy-dev"){
 //       steps {
 //            script {
  //              def public_ip = bat(returnStdout: true, script: 'terraform output public_ip').trim()
 //               sshagent(['Deploy_Auto']) {
              //public_ip= $(terraform output public_ip)
				//sh  "scp -o StrictHostKeyChecking=no C:/ProgramData/Jenkins/.jenkins/workspace/Automation_Demo/target/springbootApp.jar ec2-user@public_ip: /usr/local/tomcat9/webapps/ "
//				        bat   "ssh -o StrictHostKeyChecking=no ec2-user@public_ip tomcatdown"
//				        bat   "ssh -o StrictHostKeyChecking=no ec2-user@public_ip tomcatup"
//					}
//				}
//			}  
 //    }
}

post {     
        failure {
            mail to: 'vinayakakg7@gmail.com , vinayaka.kg@cyqurex.com',
            subject: "Build failed in ${currentBuild.fullDisplayName}",
            body: """${env.JOB_NAME} build #${env.BUILD_NUMBER} has failed.
                  Please investigate and fix the issue."""
            attachLog: true
            }
        success {
            mail to: 'vinayakakg7@gmail.com , vinayaka.kg@cyqurex.com',
            subject: "Build successful in ${currentBuild.fullDisplayName}",
            body: """${env.JOB_NAME} build #${env.BUILD_NUMBER} has succeeded.
                   Congratulations!"""
            attachLog: true
    }
  }   
}
