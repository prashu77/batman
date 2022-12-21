pipeline{
    agent any
    environment{
        staging_server="20.232.151.107"
    }   
    stages{
        stage('php-version'){
            steps  {
                sh 'php --version'
            }
        }
        stage('composer'){
            steps  {
                sh 'composer install --no-interaction --prefer-dist'
            }
        }
        stage('deploy to v2'){
            steps  {
                sh 'scp -r ${WORKSPACE}/* ibllnxreps2admin@${staging_server}:/var/www/html/'
            }
        }
    }
}
