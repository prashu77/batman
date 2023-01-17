pipeline{
    agent any
    environment{
        staging_server="20.212.167.75"
    }   
    stages{
        stage('php-version'){
            steps  {
                sh 'php --version'
            }
        }
        stage('Email Notifiacation'){
            steps  {
                mail bcc: '', body: '''Do you want to approve for the deployment then go for link below 
http://20.212.156.246:8080/job/demo/''', cc: '', from: '', replyTo: '', subject: ' approve or Abort ?', to: 'prashanthbn777@gmail.com'
            }
        }
        stage('deploy to v2'){
            steps  {
                timeout(time: 15, unit: "MINUTES") {
	                    input message: 'Do you want to approve the deployment?', ok: 'Yes'
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
        stage('email'){
            steps  {
                mail bcc: '', body: '''The committed code are deployed to server pls check . 
server url''', cc: '', from: '', replyTo: '', subject: 'files are deployed   ', to: 'prashanthbn777@gmail.com'
            }
        }
    }
}
