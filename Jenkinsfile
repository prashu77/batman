pipeline{
    agent any
    environment{
        staging_server="172.173.251.119"
        def jobName = "currentBuild.fullDisplayName"
        def mailToRecipients = 'prashanth.bn7@outlook.com'
        def useremail='prashanth.bn7@outlook.com'
    }   
    stages{
        stage('php-version'){
            steps  {
                sh 'php --version'
            }
        }
        stage('deploy to v2'){
            steps  {                
                input {
                    message "Should we continue?"
                    ok "Yes, we should."
                    submitter "prashanth"
                    parameters {
                        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                    }
                }
               sh '''
                    for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`              
                    do               
                        fil=$(echo ${fileName}  | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})          
                   scp -r ${WORKSPACE}${fil} ibllnxreps2admin@${staging_server}:/var/www/html/demo${fil}
                done
                ''' 
            }
        }
    }
}
