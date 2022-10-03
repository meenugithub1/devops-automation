pipeline {
    agent any
    tools{
        maven 'Maven 3.8.6'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/meenugithub1/devops-automation']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t meenudocker1/devops-integration .'
                }
            }
        }
        stage('push image to docker hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        bat 'docker login -u meenudocker1 -p ${dockerhubpwd}'
                        bat 'docker push meenudocker1/devops-integration'
}
                }
                
            }
        }
    }
}