pipeline {

agent any

    environment {
  registry  = "019523160407.dkr.ecr.ap-south-1.amazonaws.com/mypythonweb"
}

    stages {
        stage ('Checkout') {
            steps {
            git branch: 'main', credentialsId: 'github_key', url: 'https://github.com/rsaideekshith/simplewebrepo.git'
            }
        }
        stage ('Docker Build') {
            steps {
                script {
                    sh 'docker build -t mypythonweb:3.0 .
                }
            }
        }
        stage ('Docker Push') {
            steps {
                script {
                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 019523160407.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker push 019523160407.dkr.ecr.ap-south-1.amazonaws.com/mypythonweb:3.0'
                }
            }
        }
    }
}
