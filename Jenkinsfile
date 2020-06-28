  
pipeline {
	agent any	
	stages {
		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e ./blue/index.html'
				sh 'tidy -q -e ./green/index.html'
			}
		}
		stage('Build and Push image') {
			//This registers with DockerHub before pushing images to docker hub account
            docker.withRegistry('https://docker.mycorp.com/', 'DOCKER_HUB_CRED') {
                // docker build images
                def testblue = docker.build("ejejosh/testblueimage")
                def testblue = docker.build("ejejosh/testgreenimage")
                
                sh "docker pull --all-tags ${myImg.imageName()}"
                // runs: docker pull --all-tags docker.mycorp.com/myImg
                sh 'testblue.push("${env.BUILD_NUMBER}")'
				sh 'testblue.push("latest")'
				sh 'testgreen.push("${env.BUILD_NUMBER}")'
				sh 'testgreen.push("latest")'
			} 
			echo "Pushing Docker Build to DockerHub"
        }
	}
}			



