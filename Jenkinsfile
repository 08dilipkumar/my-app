pipeline {
    agent {
        label 'app'
    } 
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
        stage('Deploy') {
            steps {
                sh 'scp target/app.war dilip@172.17.0.4:/home/Dk/apache-tomcat-9.0.82/webapps'
            }
        }
    }
}
