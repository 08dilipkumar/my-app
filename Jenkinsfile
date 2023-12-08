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
         stage('REPORT') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }   
        stage('JACOCO-REPORT') {
            steps{
                jacoco buildOverBuild: true, changeBuildStatus: true, deltaBranchCoverage: '80', deltaClassCoverage: '80', deltaComplexityCoverage: '80', deltaInstructionCoverage: '80', deltaLineCoverage: '80', deltaMethodCoverage: '80', maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
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
        stage('DOCKER'){
            perameters {
                old_build_num='expr $BUILD_NUMBER - 1'
            }
            steps {
                sh 'docker build -t my-app:$BUILD_NUMBER .'
                sh "docker rmi my-app:$old_build_num"
            }
        }
    }
}
