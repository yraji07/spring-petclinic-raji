pipeline {
    agent { label 'MAVEN_17' }
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/yraji07/spring-petclinic-raji.git',
                    branch: 'main'
            }
        }
        stage('build') {
            steps {
                sh "mvnw package"
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