  
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
				sh './blue/run_docker.sh'
				sh './green/run_docker.sh'
			}
    	}
		stage('Push docker image') {
			steps{
				docker.withRegistry('https://registry.hub.docker.com', 'DOCKER_HUB_CREDENTIALS'){
					sh './blue/upload_docker.sh'
					sh './green/upload_docker.sh'
				}
			}
		}
	}			
}


