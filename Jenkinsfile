node() {
         
        stage('checkout repo') {
            cleanWs()
            checkout scm
            currentWs = sh(returnStdout: true, script: 'pwd').trim()
            commit_hash = sh(script: 'git rev-parse @', returnStdout: true)
            previous_commit = sh(script: 'git rev-parse @~', returnStdout: true)
            println("current commit hash :" + commit_hash)
            println("previous commit hash :" + previous_commit) 
            sh "git diff HEAD~1 deployment_tracker | grep -Po '(?<=^\\+)(?!\\+\\+).*' >> input_file"
            
        }    

        stage('read input file') {
            def line = readFile(file: 'input_file')
               service = line.split(': ')[0]
               tag = line.split(':')[1]
                def deploy  = [:]
                deploy[service] = tag


             def build = [learner:'learner_build',portal:'player_build',lp:'learning']

            for (entry in deploy) {
                    println("$entry.key : $entry.value")
                    service_to_deploy = "$entry.key"
                    build_tag = "$entry.value"
                    build_job = build[service_to_deploy]
                    println(build_job)
                    

              }

        }    
        
}
