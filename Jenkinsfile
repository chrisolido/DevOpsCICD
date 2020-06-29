pipeline {  
	environment {
		registry = "ejejosh/testgreenimage"
		registryCredential = 'DOCKER_HUB_CRED'
	}  
	agent any  
	stages{
		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./green/index.html'
			}
		}
		stage('Building image') {
			steps{
				script {
					dockerImage = docker.build registry , "-f ./green/Dockerfile ./green"
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
				sh 'kubectl apply -f ./green/green-controller.json'
				sh 'kubectl apply -f ./blue-green-service.json'
			}
			
		}
		stage('Remove Unused docker image') {
			steps{
				sh "docker rmi $registry:testblueimage"
			}
		}

	} 
}
