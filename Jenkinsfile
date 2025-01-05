pipeline {
    agent { label 'Jenkins-Agent' }

    stages {

        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-cred', toolName: 'docker') {
                        sh "docker build -t nizartheone/adservice:latest ."
                    }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub-cred', toolName: 'docker') {
                        sh "docker push nizartheone/adservice:latest "
                    }
                }
            }
        }

        stage("Trivy Scan") {
           		steps {
               			script {
	            			sh ('docker run -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image nizartheone/adservice:latest --no-progress --scanners vuln  --exit-code 0 --severity HIGH,CRITICAL --format table')
               			}
           		}
       		}

		stage ('Cleanup Artifacts') {
           		steps {
               			script {
                    			sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
                    			sh "docker rmi ${IMAGE_NAME}:latest"
               			}
          		}
       		}

    }
}
