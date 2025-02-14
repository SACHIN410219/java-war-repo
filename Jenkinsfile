pipeline {
    agent any
    stages {
                stage('Clean Up') {
                    steps {
                        cleanWs()
                    }
                }
         stage('Parallel Execution') {  
            parallel {
                stage('Clone') {
                    steps {
                        sh 'git clone https://github.com/SACHIN410219/java-war-repo.git'
                    }
                }
                stage('Build') {
                    steps {
                        dir('java-war-repo') {
                            sh 'mvn clean install -DskipTests'  
                        }
                    }
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
