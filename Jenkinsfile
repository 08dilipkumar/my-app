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
                git branch: 'main', url: 'https://github.com/08dilipkumar/my-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        } 
        stage('Deploy') {
            steps {
                sh 'scp target/app.war dilip@172.17.0.3:/home/Dk/apache-tomcat-9.0.82/webapps'
            }
        }
    }
}
