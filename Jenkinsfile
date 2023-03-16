pipeline {
    agent { label 'UBUNTU_NODE' }
    
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/yraji07/spring-petclinic-raji.git',
                    branch: 'develop'
            }
        }
        stage('build') {
            steps {
                sh "mvn package"
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    } 
}  
