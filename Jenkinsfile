pipeline {
    agent { label 'Jenkins-Agent' }

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-cred', toolName: 'docker') {
                        sh "docker build -t nizartheone/productcatalogservice:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-cred', toolName: 'docker') {
                        sh "docker push nizartheone/productcatalogservice:latest "
                    }
                }
            }
        }
    }
}
