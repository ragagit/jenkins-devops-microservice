pipeline{
	agent any
	//agent { docker { image 'node:13.6'} }
	//agent { docker { image 'maven:3.6.3'} }
	environment {
		//dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		//PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		PATH = "$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps {
				sh 'mvn --version'
				//sh 'node --version'
				sh 'docker version'
				echo "Build"
				echo "$PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "JOB_NAME -  $env.JOB_NAME"
			}
		}
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}	
	} 

	post {
		always {
			echo 'I always run'
   		}
		success {
			echo 'Successful run'
		}
		failure {
			echo 'Failure run'
		}
	}
}

