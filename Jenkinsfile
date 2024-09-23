pipeline{
	agent any
	
	stages{
		stage('Check for Changes') {
            		steps {
                		script {
					sh 'git diff'
				}
			}
		}
	}
}
