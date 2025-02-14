pipeline {
    agent any
    stages {
        stage('Parallel Execution') {  
            parallel {
                stage('Clean Up') {
                    steps {
                        cleanWs()
                    }
                }
                stage('Clone') {
                    steps {
                        sh 'git clone https://github.com/Rakesh-k-ops/java-war-repo.git'
                    }
                }
                stage('Build') {
                    steps {
                        dir('java-war-repo') {
                            sh 'mvn clean install -DskipTests'  
                        }
                    }
                }
                stage('Test') {
                    steps {
                        dir('java-war-repo') {
                            sh 'mvn test'
                        }
                    }
                }
            }
        }
    }
}
