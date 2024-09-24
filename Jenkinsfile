pipeline {
    agent any

    stages {
        stage('Check for Changes') {
            steps {
                script {
                    def commitFiles = sh(script: "git diff-tree --no-commit-id --name-only -r HEAD", returnStdout: true).trim().tokenize('\n')

                    	def new = commitFiles.findAll { file ->
                        	sh(script: "git ls-files --error-unmatch ${file}", returnStatus: true) != 0
                    }

			def deleted = commitFiles.findAll { file ->
                        	sh(script: "git ls-files --deleted --error-unmatch ${file}", returnStatus: true) == 0
                    }

			def modified = commitFiles.findAll { file ->
                        	sh(script: "git diff --name-only HEAD~1 HEAD -- ${file}", returnStatus: true) == 0
                    }

                    	def changes = new + deleted + modified

                    	if (changes) {
				def message = "The following files were changed (new or deleted):\n" + changes.join('\n')
                        	sh """
//					(echo "Subject: Files Changed in Last Commit"; 
//                             		echo "To: shadydoshita@gmail.com"; 
//                           		echo "Content-Type: text/plain"; 
                             		echo "Hello"; 
//                             		echo "${message}") | sendmail -t
                        	"""
                    	} 
                    
                }
            }
        }
    }
}
