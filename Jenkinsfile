pipeline{
	agent any
	
	stages{
		stage('Check for Changes') {
            		steps {
                		script {
					def commitFiles = sh(script: "git diff-tree --no-commit-id --name-only -r HEAD", returnStdout: true).trim().tokenize('\n')

            			echo "Changed files in the last commit: ${commitFiles.join(', ')}"
				}
			}
		}
	}
}
