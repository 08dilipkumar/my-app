pipeline {
    agent any
    triggers{
        pollSCM '* * * * *'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'ui', url: 'https://github.com/08dilipkumar/my-app.git'
            }
        } 
        stage('Build ') {
            steps {
                sh 'mvn install'
            }
        } 
       
        stage('Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'app', classifier: '', file: 'target/app-1.0-SNAPSHOT.war', type: 'war']], credentialsId: 'Nexus', groupId: 'app', nexusUrl: '172.17.0.1:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://172.17.0.1:8081/repository/MVN/', version: '1.0-SNAPSHOT'
        } 
        }
    }
}
