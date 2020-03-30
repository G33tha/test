node() {
         
         stage('checkout repo') {
            cleanWs()
            checkout scm
            commit_hash = sh(script: 'git rev-parse @', returnStdout: true)
            previous_commit = sh(script: 'git rev-parse @~', returnStdout: true)
            println("current commit hash :" + commit_hash)
            println("previous commit hash :" + previous_commit) 
            println("changes to the deployment sheet is:")
            sh "git diff HEAD~1 deployment_tracker | grep -Po '(?<=^\\+)(?!\\+\\+).*'"
        }
   
        }
