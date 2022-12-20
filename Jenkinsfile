pipeline{
    agent any
    environment{
        staging_server="20.232.151.107"
    }   
    stages{
        stage('deploy to v2'){
            steps  {
                scp -P 22 -r ${WORKSPACE}/* root@${staging_server}:/var/www/html/
            }
        }
    }
}
