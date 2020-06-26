  
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
				//sh 'docker.build("testblueimage", "-f ./blue .")'
				sh 'docker run -p 8000:80 testblueimage'
				sh '''docker build -t testgreenimage -f "./green/Dockerfile" .'''
				//sh 'docker.build("testblueimage", "-f ./green .")' 
				sh 'docker run -p 8000:80 testgreenimage'
				//sh 'docker.build("testblueimage", "-f ./green .")' 
				//sh 'docker run -p 8000:80 testgreenimage'
    		}
		}
	}
}			



