pipeline {
    agent any

    environment {
  registry  = "019523160407.dkr.ecr.ap-south-1.amazonaws.com/dockerweb"
}

    stages {
        stage ('Checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitHUB', url: 'git@github.com:rsaideekshith/simplewebrepo.git']]])
            }
        }
        stage ('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        stage ('Docker Push') {
            steps {
                script {
                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 019523160407.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker push 019523160407.dkr.ecr.ap-south-1.amazonaws.com/your_ecr_repo:latest'
                }
            }
        }
    }
}
