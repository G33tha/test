node() {
         
         stage('checkout repo') {
            cleanWs()
            checkout scm
            commit_hash = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
            println("current commit hash :" + commit_hash)
        }
   
        }
