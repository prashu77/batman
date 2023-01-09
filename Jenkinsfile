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
