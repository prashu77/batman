pipeline{
    agent any
    environment{
        staging_server="20.14.201.174"
    }   
    stages{
        stage('php-version'){
            steps  {
                sh 'php --version'
            }
        }
        stage('deploy to v2'){
            steps  {
                sh 'scp -r ${WORKSPACE}${fil} adminuser@${staging_server}:/var/www/html/demo${fil}'
            }
        }
    }
}
