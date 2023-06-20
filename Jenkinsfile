pipeline {    
    agent any
    environment {
        REGISTRY = "rolandop"
        RESULT_NAME = "voting_result"
        RESULT_VERSION = "1.1"
        VOTE_NAME = "voting_vote"
        VOTE_VERSION = "1.1"
        WORKER_NAME = "voting_worker"
        WORKER_VERSION = "1.1"
        DOCKER_HUB_LOGIN = credentials('dockerhub-rolandop')
    }
    stages {        


        stage('IoC') {
            agent {
                docker {
                    image "rolandop/ubuntu_ioc"
                    args '-u root:root'
                    reuseNode true
                }
            }
             
            steps {
                sh "apt update"
                withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS-PIN'),
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']) {
                    sh "aws --version"
                }                       
                sh "terraform --version"
                dir ("terraform"){
                    sh "echo terraform init"
                    sh "terraform init"
                }
            }
                   
        }

     }
 }
