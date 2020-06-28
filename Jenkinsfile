  
pipeline {
	agent any	
	stages {
		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./blue/index.html'
				sh 'tidy -q -e ./green/index.html'
			}
		}
		stage('Build image') {
			/* This builds the actual image */
			steps{
				sh 'testblue = docker.build("ejejosh/testblueimage")'
				sh 'testgreen = docker.build("ejejosh/testgreenimage")'
			}
			
    	}		
	
		stage('Push image') {
			/*This registers with DockerHub before pushing images to docker hub account*/
			steps{
				docker.withRegistry('https://registry.hub.docker.com', 'DOCKER_HUB_CRED') {
					testblue.push("${env.BUILD_NUMBER}")
					testblue.push("latest")
					testgreen.push("${env.BUILD_NUMBER}")
					testgreen.push("latest")
				} 
				echo "Pushing Docker Build to DockerHub"
			}				
		}
	}
}			



