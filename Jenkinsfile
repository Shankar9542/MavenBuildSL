pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh "mvn clean install -Dmaven.test.skip=true"
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war'
            }
        }

        stage('Deployment') {
            steps {
                deploy adapters: [tomcat9(url: 'http://34.228.160.139:8080/', 
                                          credentialsId: 'TomcatCreds')], 
                       war: 'target/*.war', 
                       contextPath: 'app'
            }
        }

        stage('Notification') {
            steps {
                emailext(
                    subject: "Job Completed",
                    body: "Jenkins pipeline job for Maven build job completed",
                    to: "shankarch367@gmail.com"
                )
            }
        }
    }
}
