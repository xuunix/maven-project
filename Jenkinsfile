pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh '/usr/local/apache-maven/apache-maven-3.5.3/bin/mvn clean package'
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
