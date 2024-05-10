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
		stage('push on docker-hub') {
                       steps {
                                 withCredentials([string(credentialsId: 'docker_hub_pass', variable: 'docker_hub_pass_var')]) {
                                 sh 'sudo docker login -u daemonaman -p ${docker_hub_pass_var}'
				 sh 'sudo docker push daemonaman/java-app:$BUILD_TAG'
                                 }
		       }
		}
		stage('testing the build') {
                        steps {
                                 sh 'sudo docker run -dit --name java-container$BUILD_TAG -p 8090:8080 daemonaman/java-app:$BUILD_TAG'
                       }

		}

        	}

}
