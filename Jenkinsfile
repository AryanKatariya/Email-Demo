pipeline{
	agent any
	
	stages{
		stage('Check for Changes') {
            		steps {
                		script {
					def javaVersion = sh(script: 'java -version', returnStdout: true).trim()
                    			echo "Java version: ${javaVersion}"
				}
			}
		}
	}
}
