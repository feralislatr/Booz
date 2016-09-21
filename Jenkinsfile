#!groovy

node {
        currentBuild.result = "SUCCESS"
        
        try {
                stage "Prepare environment"
                  //sh 'env | sort'
                  checkout scm
                  sh ('sudo usermod -aG docker jenkins && groups')
                  
                  sh "echo $env.BRANCH_NAME | tr '[:upper:]' '[:lower:]' > branchnamefile"
                  def branchName=readFile('branchnamefile').trim()
                  
                stage "Print Variables"
                   sh "cd .."  
                   sh "cd tmp"
                   sh "cat params.txt"
                //   sh "echo $branchName"
                //   def environment = docker.build "wine-spring-service:$branchName-$env.BUILD_ID" 
                  
                //   environment.inside {
                //     stage 'Unit Tests'
                //         sh 'mvn install'
                        
                //     if (env.BRANCH_NAME == 'master') {
                //       //temporarily commented out bc it's annoying
                //         // stage 'Manual Gate'
                //         //     def userInput = input(
                //         //         id: 'userInput', message: 'Continue to next stage?', submitter: "GSA*Pipeline"
                            
                //         //         // , parameters: [
                //         //         // [$class: 'TextParameterDefinition', defaultValue: 'uat1', description: 'Target', name: 'target']
                //         //         // ]
                //         //     ) 
                        
                //         stage 'Functional Tests'
                //         //Nothing here yet
                //     }
                    
                //     junit 'target/surefire-reports/TEST-dbDemo.PgBootApplicationTests.xml'
                //  }
                 
                 //push image - brianaslateradm/blueocean
                //sh "docker pull dockerhub-app-01.east1e.nonprod.dmz/brianaslateradm/blueocean"
                // sh "docker tag wine-spring-service:$branchName-$env.BUILD_ID dockerhub-app-01.east1e.nonprod.dmz/brianaslateradm/blueocean:$branchName-$env.BUILD_ID"
                // sh "docker push dockerhub-app-01.east1e.nonprod.dmz/brianaslateradm/blueocean:$branchName-$env.BUILD_ID"
                 
                stage 'Send Slack Message'
                slackSend color: "good", message: "Job `${env.JOB_NAME}`, build `${env.BUILD_DISPLAY_NAME}`\nBranch: ${env.BRANCH_NAME}\nCommit author: @${env.USER}\n${currentBuild.result}\nBuild report: ${env.BUILD_URL}"
        } catch (err) {
            currentBuild.result = "FAILURE"
            slackSend color: "bad", message: "Job `${env.JOB_NAME}`, build `${env.BUILD_DISPLAY_NAME}`\nBranch: ${env.BRANCH_NAME}\nCommit author: @${env.USER}\n${currentBuild.result}\nBuild report: ${env.BUILD_URL}"
            throw err
        }
}
