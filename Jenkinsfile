node() {
         
         stage('checkout repo') {
            cleanWs()
            checkout scm
            commit_hash = sh(script: 'git rev-parse @', returnStdout: true).trim()
            previous_commit = sh(script: 'git rev-parse @~', returnStdout: true).trim()     
            println("current commit hash :" + commit_hash)
            println("previous commit hash :" + previous_commit)      
        }
   
        }
