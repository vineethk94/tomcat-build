pipeline {
    agent any
    triggers {
  cron 'H/5 * * * *'
}

    tools{
        maven 'maven-3.8.6'
    }
    options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '2')
}


    stages {
        stage('Clone the repository') {
            steps {
               git credentialsId: 'Github_username_password', url: 'https://github.com/techworldwithmurali/Build-and-Push-to-artifactory.git'
            }
        }


        stage('Build the maven code') {
            steps {
            sh 'mvn clean install'
                 }
    }

stage('Deploy to tomcat') {
            steps {
            deploy adapters: [tomcat7(credentialsId: 'Tomcat_Username_password', path: '', url: 'http://15.207.117.35:8080')], contextPath: null, war: '**/*.war'
                 }
    }
}
}
