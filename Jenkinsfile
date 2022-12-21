pipeline{
    agent any
    environment{
        staging_server="172.174.75.252"
    }   
    stages{
        stage('php-version'){
            steps  {
                sh 'php --version'
            }
        }
    }
    stages{
        stage('composer'){
            steps  {
                sh 'composer install --no-interaction --prefer-dist'
            }
        }
    }
    stages{
        stage('deploy to v2'){
            steps  {
                sh 'scp -r ${WORKSPACE}/* ibllnxreps2admin@${staging_server}:/var/www/html/'
            }
        }
    }
}
