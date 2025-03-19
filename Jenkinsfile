pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1' 
        ECR_REPO = '361769602502.dkr.ecr.us-east-1.amazonaws.com/kubernates' 
                IMAGE_NAME = 'java1-app-image'
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
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Push Image to AWS ECR') {
            steps {
                script {
                    // Log in to AWS ECR
                    sh """
                    aws ecr get-login-password --region $AWS_REGION | sudo docker login --username AWS --password-stdin $ECR_REPO
                    """

                    // Tag the Docker image
                    sh "sudo docker tag $IMAGE_NAME:latest $ECR_REPO:latest"

                    // Push the Docker image to ECR
                    sh "sudo docker push $ECR_REPO:latest"
                }
            }
        }
    }
}
