pipeline {
        agent any
	stages {
                stage('pull code from git repo') {
                       steps {
                                 git branch: 'main', url: 'https://github.com/daemonaman/java-app.git'
		       }
		}
		stage('build the code') {
                       steps {
                                 sh 'sudo mvn dependency:purge-local-repository'
				 sh 'sudo mvn clean package'
		       }
		}
		stage('building docker image') {
                       steps {
                                 sh 'sudo docker build -t java-app:$BUILD_TAG .'
				 sh 'sudo docker tag java-app:$BUILD_TAG daemonaman/java-app:$BUILD_TAG'
		       }  
		}
	}
}
