pipeline {
    agent any
    triggers {
  cron 'H/5 * * * *'
}

    tools{
        maven 'Apache Maven 3.6.3'
    }
    options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '2')
}


    stages {
        stage('Clone the repository') {
            steps {
               git credentialsId: 'Github_username_password', url: 'https://github.com/vineethk94/tomcat-build.git'
            }
        }


        stage('Build the maven code') {
            steps {
            sh 'mvn clean install'
                 }
    }

stage('Deploy to tomcat') {
            steps {
            deploy adapters: [tomcat8(credentialsId: 'Tomcat_username_password', path: '', url: 'http://54.208.86.150:9090/')], contextPath: null, war: '**/*.war'
                 }
    }
}
}
