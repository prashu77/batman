pipeline{
    agent any
    environment{
        staging_server="20.232.151.107"
    }   
    stages{
        stage('deploy to v2'){
            steps  {
                sh 'scp.sh'
            }
        }
    }
}
