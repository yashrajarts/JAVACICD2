pipeline {
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yashrajarts/JAVACICD.git']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t yashrajarts/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                withCredentials([string(credentialsId: 'yashrajarts', variable: 'yashrajarts')]) {
                   bat 'docker login -u yashrajarts -p ${yashrajarts}'
                }
                  // bat 'docker push yashrajarts/devops-integration'
                }
            }
//        stage('Deploy to k8s'){
  //          steps{
    //            script{
      //              kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
        //        }
//          //  }
        }
    }
}
