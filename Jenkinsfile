pipeline{
	agent any
	environment{
		DOCKERHUB_CRED=credentials('dockerhubID')
		IMAGE_NAME='josh57/exam4'
	}
	stages{
	stage('Checkout')
	{
		steps{
			git(url:'https://github.com/Lab_Test',branch:'main')
		}
	}
	stage('Build Docker')
	{
		steps{
		script{
			docker_Image=doker.build("${IMAGE_NAME}:latest")
		}
	}
	}
	stage('Push to Docker')
	{
		steps{
			script{
		
	docker.withRegistry('https://registry.hub.docker.com','dockerhubID'){
			docker_Image.push()
		}
		}
		}
	}
	}
	post{
		success{
		echo "Success"
	}
		failure{
		echo "Failure"
	}
		always{
		echo "Cleaning up workspace ...."
		deleteDir()
	}
	}
}
