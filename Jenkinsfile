pipeline{
    agent any
    environment{
        staging_server="20.163.238.190"
    }   
    stages{
        stage('php-version'){
            steps  {
                sh 'php --version'
            }
        }
        stage('deploy to v2'){
            steps  {
                sh 'scp -r ${WORKSPACE}/* root@${staging_server}:/var/www/html/'
            }
        }
    }
}
