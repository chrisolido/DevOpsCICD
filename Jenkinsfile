  
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
	}
}			



