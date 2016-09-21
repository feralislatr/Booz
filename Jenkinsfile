#!groovy

node {
        currentBuild.result = "SUCCESS"
        
        try {
                stage "Prepare environment"
                  //sh 'env | sort'
                  checkout scm
                  //sh ('sudo usermod -aG docker jenkins && groups')
                  
                  sh "echo $env.BRANCH_NAME | tr '[:upper:]' '[:lower:]' > branchnamefile"
                  def branchName=readFile('branchnamefile').trim()
                  
                stage "Print Variables"
                   sh "cd"  
                   sh "scp tmp/params.properties /var/lib/jenkins/workspace"
                   
                   sh('cat /params.properties > COMMENT')
                   def stdout = readFile('COMMENT').trim()

        } catch (err) {
            throw err
        }
}
