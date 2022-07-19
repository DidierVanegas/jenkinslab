pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub_cred')
    }
    
    stages {
        stage("Image building") {
            steps {
                sh 'docker build -t dvanegas/webserver:latest .'
            }
        }
        stage("Dockerhub login") {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage("Image push") {
            steps {
                sh 'docker push dvanegas/webserver:latest'
            }
        }
        stage("Cleaning up") {
            steps {
                sh "docker rmi dvanegas/webserver:latest"
            }
        }
    }

    post {
		always {
			sh 'docker logout'
		}
	}
}