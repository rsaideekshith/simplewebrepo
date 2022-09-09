pipeline {

agent any

    environment {
  registry  = "019523160407.dkr.ecr.ap-south-1.amazonaws.com/pythonweb"
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
                    sh 'docker build -t pythonweb .'
                    sh 'docker tag pythonweb:latest 019523160407.dkr.ecr.ap-south-1.amazonaws.com/pythonweb:3.0'
                }
            }
        }
        stage ('Docker Push') {
            steps {
                script {
                    sh 'docker login -u AWS -p $(aws ecr get-login-password --region ap-south-1) 019523160407.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker push 019523160407.dkr.ecr.ap-south-1.amazonaws.com/pythonweb:3.0'
                }
            }
        }
    }
}

stage ('Deploy' ) {
    steps {
        script {
             'aws ecs update-service --service pythonapp --force-new-deployment --cluster pythonform --region ap-south-1'
        }
    }
}
