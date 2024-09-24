pipeline {
    agent any

    stages {
        stage('Check for Changes') {
            steps {
                script {
                    // Get the list of changed files
                    def commitFiles = sh(script: "git diff-tree --no-commit-id --name-only -r HEAD", returnStdout: true).trim().tokenize('\n')

                    // Identify new files
                    def newFiles = commitFiles.findAll { file ->
                        sh(script: "git ls-files --error-unmatch ${file}", returnStatus: true) != 0
                    }

                    // Identify deleted files
                    def deletedFiles = commitFiles.findAll { file ->
                        sh(script: "git ls-files --deleted --error-unmatch ${file}", returnStatus: true) == 0
                    }

                    // Identify modified files
                    def modifiedFiles = commitFiles.findAll { file ->
                        sh(script: "git diff --name-only HEAD~1 HEAD -- ${file}", returnStatus: true) == 0
                    }

                    // Combine all changes
                    def changes = newFiles + deletedFiles + modifiedFiles

                    // If there are any changes, prepare and send the message
                    if (changes) {
                        def message = "The following files were changed (new, deleted, or modified):\n" + changes.join('\n')

                        // Using emailext to send the email
                        emailext(
                            to: "shadydoshita@gmail.com",
                            subject: "Files Changed in Last Commit",
                            body: message
                        )
                    } else {
                        echo 'No new, deleted, or modified files found.'
                    }
                }
            }
        }
    }
}

