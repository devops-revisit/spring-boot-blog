pipeline
{
	agent any
	tools
	{
		maven "maven3.9"
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
	}
}
