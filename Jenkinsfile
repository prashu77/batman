pipeline{
    agent any
    environment{
        staging_server="20.115.14.150"
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
