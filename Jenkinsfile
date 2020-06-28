pipeline {  
	environment {
		registry = "ejejosh/testblueimage"
		registryCredential = 'DOCKER_HUB_CRED'
	}  
	agent any  

	stages {
		stage('Building image') {
			steps{
				script {
					docker.build registry + "-tag=testblueimage", ":$BUILD_NUMBER", "-f ./blue/Dockerfile ./blue"
				}
			}
		}
    }
}
