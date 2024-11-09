pipeline {
	agent {  
		docker { 
			image 'luiskywalker/javamav:release1' 
			reuseNode true
		} 
	}
	stages {
		stage('Checkout') {
            steps {
				sh 'mvn --version'
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD_ID - $env.BUILD_ID"
                echo "JOB_NAME - $env.JOB_NAME"
                echo "BUILD_TAG - $env.BUILD_TAG"
                echo "BUILD_URL - $env.BUILD_URL"
            }
        }
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	} 
	post {
		always {
			echo 'I run always'
		}
		success {
			echo 'I run when success'
		}
		failure {
			echo 'I run when fails'
		}
	}
}
