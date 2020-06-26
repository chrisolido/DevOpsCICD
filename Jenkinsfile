  
pipeline {
	agent any
	stages {
		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./blue/index.html'
				sh 'tidy -q -e ./green/index.html'
			}
		}		
		stage('Build Blue Image') {	
			steps{	
				sh '''docker build -t testblueimage -f "./blue/Dockerfile"'''
				sh 'docker run -p 8000:80 testblueimage'
    		}
		}				
		stage('Build Green Image') {	
			steps{	
				sh '''docker build -t testgreenimage -f "./green/Dockerfile"'''
				sh 'docker run -p 8000:80 testgreenimage'
    		}
		}
	}
}			



