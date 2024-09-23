pipeline{
	agent any

	tools {
        	jdk 'JAVA_17'
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
