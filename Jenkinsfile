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
				git branch: 'main', url: ''	
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
		stage('SonarQube Analysis') {
			steps{

			}
		}
		stage('Quality Gate') {
			steps{

			}
		}
		stage('Build') {
			steps{
				sh "mvn package"
			}
		}
		stage('Publish To Nexus') {
			steps{
				sh "mvn deploy"
			}
		}
		stage('Build & Tag Docker Image') {
			steps{
				sh "docker build -t username/app:latest ."
			}
		}
		stage('Docker Image Scan') {
			steps{
				sh "trivy image --format table -o trivy-di-report.html username/app:latest"
			}
		}
		stage('Push Docker Image') {
			steps{
				sh "docker push username/app:latest"
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

