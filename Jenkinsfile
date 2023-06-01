pipeline{
    agent 'any'
    stages{
        stage('VCS'){
            steps{
                git url: 'https://github.com/yraji07/spring-petclinic-raji.git',
                    branch: 'ci-cd'
            }
        }
        stage('build'){
            steps{
                sh './mvnw package'
            }
        }
        stage("junit"){
            steps{
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                    onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
        stage('docker'){
            steps{
                sh 'sudo docker image build -t spc .'
                sh 'sudo docker image tag spc raji07/rajispringpetclinic:latest'
                sh 'sudo docker image push raji07/rajispringpetclinic:latest'
            }
        }
        stage('deployment'){
            steps{
                sh 'kubectl apply -f manifest.yaml'
                sh 'kubectl get all'
            }
        }
    }
}
