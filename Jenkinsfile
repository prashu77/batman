pipeline{
    agent any
    environment{
        staging_server="20.115.14.150"
    }  
def jobName = currentBuild.fullDisplayName
def mailToRecipients = 'prashanth.bn7@outlook.com'
def useremail='prashanth.bn7@outlook.com' 
    stages{
        stage('php-version'){
            steps  {
                sh 'php --version'
            }
        }
        stage('deploy to v2'){
            steps  {
            {
   def userAborted = false

 emailext body: '''
    Please go to console output of ${BUILD_URL}input to approve or Reject.<br>
 ''',    
    mimeType: 'text/html',
    subject: "[Jenkins] ${jobName} Build Approval Request",
    from: "${useremail}",
    to: "${mailToRecipients}",
    recipientProviders: [[$class: 'CulpritsRecipientProvider']]

  try { 
    userInput = input submitter: 'prashanth', message: 'Do you approve?'
 } catch (org.jenkinsci.plugins.workflow.steps.FlowInterruptedException e) {
   cause = e.causes.get(0)
   echo "Aborted by " + cause.getUser().toString()
   userAborted = true
    echo "SYSTEM aborted, but looks like timeout period didn't complete. Aborting."
 }
    if (userAborted) {
  currentBuild.result = 'ABORTED'
 }
           sh '''
                    for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`              
                    do               
                        fil=$(echo ${fileName}  | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})          
                   scp -r ${WORKSPACE}/* root@${staging_server}:/var/www/html/demo${fil}
                done
                '''
}
                
            }
        }
    }
}
