pipeline {  
	environment {
		registry = "ejejosh/testblueimage"
		registryCredential = 'DOCKER_HUB_CRED'
	}  
	agent any  
	stages{
		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./blue/index.html'
			}
		}
		stage('Building image') {
			steps{
				script {
					dockerImage = docker.build registry + ":BUILD_NUMBER", "-f ./blue/Dockerfile ./blue"
				}
			}
		}
		stage('Push Image to Docker Hub') {
			steps{
				script {
					docker.withRegistry( '', registryCredential ) {
						dockerImage.push()
					}
				}
			}
		} 
		stage("Deploy Apllication in K8S Cluster"){
			steps{
				sh 'kubectl apply -f ./blue-green-service.json'
			}
			
		}

	} 
}
