pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1' 
        ECR_REPO = '156041435862.dkr.ecr.us-east-1.amazonaws.com/java-repo:latest'
        IMAGE_NAME = 'java-app-image'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Rakesh-k-ops/java-war-repo.git'
            }
        }

        stage('Build Java Application') {
            steps {
                sh 'mvn clean package -DskipTests' 
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'sudo docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Image to AWS ECR') {
            steps {
                script {
                    sh '''
                    aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
                    docker tag $IMAGE_NAME:latest $ECR_REPO/$IMAGE_NAME:latest
                    docker push $ECR_REPO/$IMAGE_NAME:latest
                    '''
                }
            }
        }
    }
}
