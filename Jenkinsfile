pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '52.56.50.228', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '35.177.176.30', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

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

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i /stuff/maven/maven-project/JP-jenkins-kp.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i /stuff/maven/maven-project/JP-jenkins-kp.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat/webapps"
                    }
                }
            }
        }
    }
}
