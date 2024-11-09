pipeline {
	agent any
	stages {
		stage('Maven Install') {
			agent {  
				docker { 
					image 'luiskywalker/javamav:release1' 
					reuseNode true
				} 
			}
            steps {
				sh 'ls -la'
				sh 'mvn --version'
                echo "PATH - $PATH"
                echo "BUILD_NUMBER - $env.BUILD_NUMBER"
                echo "BUILD_ID - $env.BUILD_ID"
                echo "JOB_NAME - $env.JOB_NAME"
                echo "BUILD_TAG - $env.BUILD_TAG"
                echo "BUILD_URL - $env.BUILD_URL"
				sh 'ls -la'
            }
        }
		stage('Compile'){
			agent {  
				docker { 
					image 'luiskywalker/javamav:release1' 
					reuseNode true
				} 
			}
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			agent {  
				docker { 
					image 'luiskywalker/javamav:release1' 
					reuseNode true
				} 
			}
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			agent {  
				docker { 
					image 'luiskywalker/javamav:release1' 
					reuseNode true
				} 
			}
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			agent {  
				docker { 
					image 'luiskywalker/javamav:release1' 
					reuseNode true
				} 
			}
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage ('Build Docker Image'){
			steps {
				//"docker build -t luiskywalker/currency-exchange-devops:$env.BUILD_TAG"//This is a way of do this
				script { //creating a script is a more modern way to do the same thing
					dockerImage = docker.build("luiskywalker/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage ('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('', 'dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
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
