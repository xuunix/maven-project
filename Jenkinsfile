pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'export JAVA_HOME=/stuff/java/jdk1.8.0_161;/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/localMaven/bin/mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to staging'){
            steps {
                build job: 'deploy-to-staging'
            }
        }
        stage ('Deploy to production'){
            steps {
                timeout(time:5, unit:'DAYS'){
                    input message: 'Approve production deployment?'
                }

                build job: 'deploy-to-prod'
            }
            post {
                success {
                    echo 'Deployed to Production'
                }

                failure {
                    echo 'Deployment FAIL!'
                }
            }
        }
    }
}
