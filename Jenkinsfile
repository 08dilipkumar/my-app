pipeline {
    agent any 

    stages {
        stage('CLONE') {
            steps {
                git branch: 'main', url: 'https://github.com/08dilipkumar/my-app.git'
            } 
        }
        stage('CLEAN') {
            steps {
                sh 'mvn clean' 
                sh 'mvn compile'
            }
        } 

        stage('TEST') {
            steps {
                sh 'mvn test'
            }
        } 
        stage('Checkstyle Analysis') {
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }   
        stage('BUILD') {
            steps {
                sh 'mvn package'
            } 
            post {
                success {
                    echo "ArchiveArtifacts" 
                    archiveArtifacts artifacts: 'target/app.war', followSymlinks: false 

                }

            }
        }  
        stage('K8s') {
            steps {
                script{
                 sh './K8s.sh'
            }
        }
    } 
} 
}
