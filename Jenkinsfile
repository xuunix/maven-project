pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                #sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/localMaven/apache-maven-3.5.3/bin/mvn clean package'
                sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/localMaven/bin/mvn clean package'
                sh 'mvn clean package'
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
