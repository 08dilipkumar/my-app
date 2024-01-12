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
        stage('DOCKER IMAGE') {
            steps {
                sh 'docker build -t 07dilip/app:${BUILD_NUMBER} .  '
            }  
        }  
        stage('docker push') {
            steps{
                script{
                    withCredentials([string(credentialsId: 'myapp', variable: 'docker')]) {
                        script{
                            sh 'docker login -u 07dilip -p ${docker}'
                        } 
                } 
                sh 'docker push 07dilip/app:${BUILD_NUMBER}'
            } 
        }
    }  
        stage('DEPLOY-K8s'){
            steps{
                sh 'helm install my-app-release app-0.1.0.tgz'
            }
        }

    } 
}
