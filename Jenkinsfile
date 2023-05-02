pipeline {
    agent any
    tools{
        maven 'MAVEN'
    }
    stages{
        stage('Build Maven'){
            steps{
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '4fcdb2bd-fb6d-4198-aa5d-9b556ab7fcdb', url: 'https://github.com/Vinaykkumar/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t vinaykkumar/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                sh 'docker login -u vinaykkumar -p ${dockerhubpwd}'
}
                   sh 'docker push vinaykkumar/devops-integration'
                }
            }
        }
    }
}
