//DECLARATIVE
pipeline{
	agent any
	stages {
		stage('Build'){
			steps {
				echo "Build"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps {
				echo "Integration Test"
			}
		}
	} post {
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