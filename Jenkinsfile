pipeline {
	agent any
	stages {
	    stage ('clean up') {
	        steps {
	            cleanWs()
	        }
	    }
	    stage ('clone') {
			steps {
				sh 'git clone https://github.com/SACHIN410219/java-war-repo.git'
			}
		
		}
		stage ('build') {
			steps {
			    dir ('java-war-repo'){
				   sh 'mvn clean install -DskipTests'
			    }
			}
		
		}
		stage ('test') {
			steps {
			    dir ('java-war-repo'){
				    sh 'mvn test'
			    }
			}
		}
	}
}
