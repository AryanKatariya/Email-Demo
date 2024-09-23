pipeline {
    agent any

    stages {
        stage('Check for Changes') {
            steps {
                script {
                    def commitFiles = sh(script: "git diff-tree --no-commit-id --name-only -r HEAD", returnStdout: true).trim().tokenize('\n')

                    def newFiles = commitFiles.findAll { file ->
                        sh(script: "git ls-files --error-unmatch ${file}", returnStatus: true) != 0
                    }

			def deletedFiles = commitFiles.findAll { file ->
                        	sh(script: "git ls-files --deleted --error-unmatch ${file}", returnStatus: true) == 0
                    	}

			def changes = newFiles + deletedFiles

			if (changes) {
                    		sh 'whoami'
			} 
#                    if (newFiles) {
#                        mail to: "ashuverma0499@gmail.com",
#                             subject: "New Files Committed",
#                             body: "The following new files were committed:\n" + newFiles.join('\n')
#                    } else {
#                        echo 'No new files committed.'
#                    }
                }
            }
        }
    }
}

