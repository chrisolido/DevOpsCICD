  
pipeline {
	agent any
	stages {
		stage('Lint HTML') {
			steps {
				sh "tidy -q -e ./blue/index.html"
				sh "tidy -q -e ./green/index.html"
			}
		}
    }
}

