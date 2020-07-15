pipeline {
    environment {
		VERSION = "$(BUILD_NUMBER)"
		PROJECT = "demo-app"
		IMAGE = "$PROJECT:$VERSION"
		ECRURL = '077730327954.dkr.ecr.ap-south-1.amazonaws.com/demo-app'
		ECRCRED = 'awsecrcredentials'
	}
	
    agent any
	stages {
        stage('SCM Checkout') {
            steps {
            // Get source code from Gitlab repository
            
				git 'https://github.com/shareef242/real-project.git'
            }
        }

        stage('Image Build') {
			steps {
				script {  
					docker.build('$IMAGE')
				}
			}
		}
	  
		stage('Push Image') {
			steps {
				script {
					docker.withRegistry(ECRURL, ECRCRED)
						{
							docker.image(IMAGE).push()
				  
						}
					}
				}
			}
		}
	}
}