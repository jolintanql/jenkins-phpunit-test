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
            junit 'tests/junit-report.xml'
            archiveArtifacts artifacts: '**/junit-report.xml', allowEmptyArchive: true
        }

        success {
            echo 'Build and tests succeeded!'
            // Add more post-success steps here, such as notifications
        }

        failure {
            echo 'Build or tests failed.'
            // Add more post-failure steps here, such as notifications
        }

        cleanup {
            echo 'Cleaning up...'
            // Add cleanup steps here
        }
    }