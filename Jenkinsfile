pipeline
{
	agent any
	tools
	{
		maven "maven3.9"
	}
	environment
	{
		IMAGE_NAME = "blog-app"
		CONTAINER_NAME = "blog-app"
		PORT = "8091"
	}
	stages
	{
		stage('Checkout') {
			steps {
				git credentialsId: 'github', url: 'https://github.com/devops-revisit/spring-boot-blog.git'
			}
		}
		stage('Build') {
			steps {
				sh 'mvn clean package -DskipTests'
			}
		}
		stage('Verify Build') {
			steps {
				sh 'ls -l target/'
			}
		}
		stage('Docker Image') {
			steps {
				dir('docker') {
					sh 'docker build -t mnidevops/${IMAGE_NAME}:${BUILD_NUMBER} .'
				}
			}	
		}
	}
}
