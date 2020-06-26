  
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
				//sh '''docker build -t testblueimage -f "./blue/Dockerfile" .'''
				//sh '''docker build -t testblueimage -f "./green/Dockerfile" .'''
    		}
		}
		stage('Build Push Images') {	
			
			docker.withRegistry('https://registry.hub.docker.com', 'DOCKER_HUB_CREDENTIALS') {      
				sh '''./blue/upload_docker.sh'''
				sh '''./green/upload_docker.sh'''
			}
		}
	}
}			



