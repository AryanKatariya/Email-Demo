pipeline{
	agent any

	tools {
        	jdk 'JAVA_HOME'
   	 }	
	
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
