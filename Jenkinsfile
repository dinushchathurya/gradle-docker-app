pipeline {
    
    agent { 
        label 'Slave' 
        
    }
    
    stages {
        
		stage('Checkout Code') {
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/dinushchathurya/gradle-docker-app.git']]])
			}
		}
		
	    stage('Build Gradle') {
            steps {
                sh './gradlew build'
            }
	    }
	    
	    stage('Build Docker Image') {
	        steps {
	            sh './gradlew docker'
	        }
	    }
	    
	    stage('Tag Docker Image') {
	        steps {
	             sh './gradlew dockerTagDockerHub '
	        }
	    }
	    
        stage('Push image') {
            steps {
                withDockerRegistry([ credentialsId: "dockerhub", url: "https://index.docker.io/v1/" ]) {
                    sh './gradlew dockerPush'
                }
            }
        }
	 
	}
}