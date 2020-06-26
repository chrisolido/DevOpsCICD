  
pipeline {
	environment {
		registry = "ejejosh/pipeline"
		registryCredential = ‘MY_DOCKER_HUB’
	}
	agent any
	stages {
		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./blue/index.html'
				sh 'tidy -q -e ./green/index.html'
			}
		}

		stage('Building image') {
			steps{
				script {
					docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage('Deploy Image') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						dockerImage.push()
					}
				}
			}
		}		
	}
}			



