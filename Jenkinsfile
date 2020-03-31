
def trigger_build(job_name,tag) {
    println("triggering build " + job_name + " from the tag " + tag) 
    build(job: "Build/$job_name", parameters: [string(name: 'github_release_tag', value: "$tag")],wait: false)
}
           

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

        stage('read input file and trigger build') {
            def line = readFile(file: 'input_file')
               service = line.split(':')[0]
               tag = line.split(':')[1]
                def deploy  = [:]
                deploy[service] = tag


            def build = [learner:'learner_build',portal:'player',lp:'learning']

            for (entry in deploy) {
                    service_to_deploy = "$entry.key"
                    build_tag = "$entry.value"
                    build_job = build[service_to_deploy]
                    println(build_job)
                    trigger_build(build_job,build_tag)
              }

        }
        
        
}
