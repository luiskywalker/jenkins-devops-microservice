pipeline {
	agent any
	// agent {  
	// 	docker { 
	// 		image 'luiskywalker/javamav:release1' 
	// 		reuseNode true
	// 	} 
	// }
	//agent any
	// environment {
	// 	dockerHome = tool 'myDocker'
	// 	mavenHome = tool 'myMaven'
	// 	PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	// }
	stages {
		stage('Checkout') {
			//agent any
            // tools {
			// 	jdk 'Java8u202'
			// }
			 agent {
                docker {
                    image 'luiskywalker/javamav:release1'
                    reuseNode true
                }
            }
            steps {
				
				sh 'mvn --version'
				//sh 'docker version'
				//sh 'java --version'
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD_ID - $env.BUILD_ID"
                echo "JOB_NAME - $env.JOB_NAME"
                echo "BUILD_TAG - $env.BUILD_TAG"
                echo "BUILD_URL - $env.BUILD_URL"
				sh "mvn clean compile"
				sh "mvn test"
				sh "mvn failsafe:integration-test failsafe:verify"
            }
        }
		stage('Compile'){
			steps {
				//sh "mvn clean compile"
				echo 'compile temp'
			}
		}
		stage('Test') {
			steps {
				//sh "mvn test"
				echo 'test temp'
			}
		}
		// stage('Integration Test') {
		// 	steps {
		// 		sh "mvn failsafe:integration-test failsafe:verify"
		// 	}
		// }
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
