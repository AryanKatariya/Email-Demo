pipeline {
    agent any

    stages {
        stage('Check for Changes') {
            steps {
                script {
                    // Get the list of files changed in the last commit
                    def commitFiles = sh(script: "git diff-tree --no-commit-id --name-only -r HEAD", returnStdout: true).trim().tokenize('\n')

                    // Identify new files (not tracked)
                    def newFiles = commitFiles.findAll { file ->
                        sh(script: "git ls-files --error-unmatch ${file}", returnStatus: true) != 0
                    }

                    // Identify deleted files
                    def deletedFiles = commitFiles.findAll { file ->
                        sh(script: "git ls-files --deleted --error-unmatch ${file}", returnStatus: true) == 0
                    }

                    // Combine new and deleted files
                    def changes = newFiles + deletedFiles

                    // Check and act if there are changes
                    if (changes) {
                        // Print the current user as a debug step
                        sh 'whoami'

                    } 
                    
                }
            }
        }
    }
}

