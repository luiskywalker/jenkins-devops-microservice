pipeline {
	agent {  
		docker { 
			image 'maven:3.3.3' 
		} 
	}
	stages {
		stage('log.version.info'){
			steps {
				sh "mvn --version"
				echo "Build"
			}
		}
	} 
	post {
		always {
			echo ('Im awesome. I run always')
		}
		success {
			echo ('I run when it is successful')
		}
		failure {
			echo ('I run when it fails')
		}
	}
}