pipeline {
	agent {
		docker {
			image 'composer:latest'
		}
	}
	stages {
		stage('Build') {
			steps {
				sh 'composer install'
			}
		}
		stage('Test') {
			steps {
				sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
			}
		}
	}

	post {
		always {
		
			junit 'logs/unitreport.xml'		}
		success {
			echo 'Build and tests succeeded!'
		}
		failure {
			echo 'Build or tests failed.'
		}
		cleanup {
			echo 'Cleaning up...'
		}
	}
}
