pipeline {  
	environment {
		registry = "ejejosh/testblueimage"
		registryCredential = 'DOCKER_HUB_CRED'
		${env.PATH} = "./blue/Dockerfile"
	}  
	agent any  

	stages {
		stage('Building image') {
			steps{
				script {
					docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
    }
}
