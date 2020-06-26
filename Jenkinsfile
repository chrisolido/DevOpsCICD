  
pipeline {
	agent any
	stages {
		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./blue/index.html'
				sh 'tidy -q -e ./green/index.html'
			}
		}		
		stage('Build Docker Images') {	
			steps{	
				sh '''docker build -t testblueimage -f "./blue/Dockerfile" .'''
				sh '''docker build -t testgreenimage -f "./green/Dockerfile" .'''
    		}
		}
		stage('Build Push Images') {
			steps {
				withDockerRegistry([ credentialsId: "docker_hub_cred", url: "https://registry.hub.docker.com" ]) {
					sh 'docker push ejejosh/testblueimage'
					sh 'docker push ejejosh/testgreenimage'
				}
			}
		}
	}
}			



