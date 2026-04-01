pipeline
{
	agent any
	tools
	{
		maven "maven3.9"
	}
	environment
	{
		IMAGE_NAME = "spring-boot-blog"
		CONTAINER_NAME = "spring-boot-blog""
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
				sh 'docker build -t mnidevops/$IMAGE_NAME:$BUILD_NUMBER -f docker/Dockerfile .'
				
			}	
		}
		stage('Docker Push') {
			steps {
				withCredentials([usernamePassword(
	            		credentialsId: 'docker-creds',
        	    		usernameVariable: 'DOCKER_USER',
            			passwordVariable: 'DOCKER_PASS'
        			)]) {
					sh '''
					echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin
         		   		docker push mnidevops/spring-boot-blog:${BUILD_NUMBER}
					'''
					}
				}
		}
	}
}
