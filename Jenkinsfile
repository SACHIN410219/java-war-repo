pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1' 
        ECR_REPO = '361769602502.dkr.ecr.us-east-1.amazonaws.com/kubernates' 
                IMAGE_NAME = 'kubernates'
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
                sh "docker build -t kubernates ."
            }
        }

        stage('Push Image to AWS ECR') {
            steps {
                script {
                    // Log in to AWS ECR
                    sh """
                    aws ecr get-login-password --region us-east-1 | sudo docker login --username AWS --password-stdin 361769602502.dkr.ecr.us-east-1.amazonaws.com
                    """

                    // Tag the Docker image
                    sh "sudo docker tag kubernates:latest 361769602502.dkr.ecr.us-east-1.amazonaws.com/kubernates:latest"

                    // Push the Docker image to ECR
                    sh "sudo docker push 361769602502.dkr.ecr.us-east-1.amazonaws.com/kubernates:latest"
                }
            }
        }
    }
}
