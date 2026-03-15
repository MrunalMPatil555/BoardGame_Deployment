pipeline {
	agent any

	tools {
		jdk 'jdk17'
		maven 'maven3'
	}
	environment {
		SCANNER_HOME= tool 'sonar-scanner'
	}

	stages {
		stage('Git Checkout') {
			steps{
				git branch: ‘main’, credentialsID: ‘credential_name’, url: ‘https://github.com/complete_url_of_your_git_repository’	
			}
		}
		stage('Compile') {
			steps{
				sh "mvn compile"
			}
		}
		stage('Test') {
			steps{
				sh "mvn test"
			}
		}
		stage('File system scan') {
			steps{
			       sh “trivy fs –format table trivy-fs-report.html .”	
			}
		}
		stage('SonarQube Analysis') {
			steps{
				withSonarQubeEnv(‘sonar’) {
	            	sh ‘’’ $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=give_your_project_name -Dsonar.projectKey=same_as_project_name -Dsonar.java.binaries=. ‘’’
			
				}
		    }
		}
		stage('Quality Gate') {
			steps{
				script{
			       waitForQualityGate abortPipeline: false, credentialsId: ‘sonar-token’	
                }
			}
		}
		stage('Build') {
			steps{
				sh "mvn package"
			}
		}
		stage('Publish To Nexus') {
			steps{
				withMaven(globalMavenSettingsConfig: ‘global-settings’, jdk: ‘jdk17’, maven: ‘maven3’, mavenSettingsConfig:”, traceability: true) {
					sh "mvn deploy"
				}
			}
		}
		stage('Build & Tag Docker Image') {
			steps{
				script{
			      withDockerRegistry(credentialsId: ‘docker-cred’, toolName: ‘docker’) {
						sh "docker build -t username/image_name:tag ."
				  }
			    }
		    }  
		}
		stage('Docker Image Scan') {
			steps{
				sh "trivy image --format table -o trivy-image-report.html username/image_name:tag"
			}
		}
		stage('Push Docker Image') {
			steps{
				sh "docker push docker_hub_username/image_name:tag"
			}
		}
		stage('Deploy to Kubernetes') {
			steps{
				sh "kubectl apply -f deployment-service.yaml"
			}
		}
		stage('Verify the Deployment') {
			steps{
				sh "kubectl get pods"
				sh "kubectl get svc"
			}
		}
	}

	post {
        success {
            echo "Build Success"
        }
        failure {
            echo "Build Failed"
        }
    }
}

