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
        stage('deploy to v2'){
            steps  {
                post{
        always{
            mail to: "prashanthbn777@gmail.com",
            subject: "approval or abort",
            body: pls go to link for approval or abort "http://20.124.35.24:8080/job/dev/",
        }
    }
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
