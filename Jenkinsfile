pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/localMaven/apache-maven-3.5.3/bin/mvn clean package'
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
