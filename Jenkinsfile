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

                    def modifiedFiles = commitFiles.findAll { file ->
                        sh(script: "git diff --name-only HEAD~1 HEAD -- ${file}", returnStatus: true) == 0
                    }

                    def changes = newFiles + deletedFiles + modifiedFiles

                    if (changes) {
                        def message = "The following files were changed (new, deleted, or modified):\n" + changes.join('\n')

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

