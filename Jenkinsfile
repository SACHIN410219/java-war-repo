pipeline {
    agent { label 'sachin' }
    environment {
        AWS_REGION = 'us-east-1' 
        ECR_REPO = '879381244497.dkr.ecr.us-east-1.amazonaws.com/jenkins-build' 
        IMAGE_NAME = 'jenkins-app-image'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/SACHIN410219/java-war-repo.git'
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
                    
                    sh """
                    aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
                    """

                
                    sh "docker tag $IMAGE_NAME:latest $ECR_REPO:latest"

              
                    sh "docker push $ECR_REPO:latest"
                }
            }
        }
    }
}
