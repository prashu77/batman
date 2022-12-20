pipeline{
    agent any
    environment{
        staging_server="20.115.120.119"
    }   
    stages{
        stage('deploy to v2'){
            steps  {
                sh 'scp -r ${WORKSPACE}/* root@${staging_server}:/var/www/html/'
            }
        }
    }
}
