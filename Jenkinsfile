pipeline {
    agent any
    tools{
        maven 'local_mvn'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/gurudattshahane/docker-jenkins-pipeline.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t gurudattshahane/devops-integration .'
                }
            }
        }
        stage('Push Docker image to Docker Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u gurudattshahane -p ${dockerhubpwd}'

}
                   sh 'docker push gurudattshahane/devops-integration'
                }
            }
        }
    }
}