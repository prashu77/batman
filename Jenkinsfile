pipeline{
    agent any
    environment{
        staging_server="172.173.251.119"
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
http://20.124.35.24:8080/job/dev/''', cc: '', from: '', replyTo: '', subject: ' approve or Abort ?', to: 'prashanthbn777@gmail.com'
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
    }
}
