pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
		jdk 'Java17'
		maven 'Maven3'
	}

    stages {

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-cred', toolName: 'docker') {
                        sh "docker build -t nizartheone/cartservice:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-cred', toolName: 'docker') {
                        sh "docker push nizartheone/cartservice:latest "
                    }
                }
            }
        }


    }
}
