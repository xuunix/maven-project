pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh '`which mvn` clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
