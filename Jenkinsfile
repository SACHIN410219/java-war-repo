pipeline {
    agent any
    stages {
        stage('Clean Up') {
            steps {
                cleanWs()
            }
        }
        stage('Parallel Execution') {  
            steps {
                parallel (
                    Clone: {
                        stage('Clone') {
                            steps {
                                sh 'git clone https://github.com/Rakesh-k-ops/java-war-repo.git'
                            }
                        }
                    },
                    Build: {
                        stage('Build') {
                            steps {
                                dir('java-war-repo') {
                                    sh 'mvn clean install -DskipTests'
                                }
                            }
                        }
                    }
                )
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
