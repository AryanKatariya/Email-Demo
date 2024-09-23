pipeline{
	agent any
	
	stages{
		stage('Check for Changes') {
            		steps {
                		script {
                    			checkout scm
					def user = sh(script: 'whoami', returnStdout: true).trim()
                    			echo "Current user: ${user}"
				}
			}
		}
	}
}
