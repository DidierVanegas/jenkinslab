pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub_cred')
    }

    triggers {
        githubPush()
    }
    
    stages {
        stage("Image building") {
            steps {
                sh 'docker build -t dvtdev/webserver:latest .'
            }
        }
        stage("Dockerhub login") {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage("Image push") {
            steps {
                sh 'docker push dvtdev/webserver:latest'
            }
        }
        stage("Cleaning up") {
            steps {
                sh "docker rmi dvtdev/webserver:latest"
            }
        }
    }

    post {
		always {
			sh 'docker logout'
		}
	}
}