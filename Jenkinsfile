pipeline {
    agent any
    stages {
stage('Build') {
	steps {
		echo "RunningBuild automation"
		sh './gradlew build --no-daemon'
		archiveArtifacts artifacts: 'dist/trainSchedule.zip'
		}
	}
stage('Build Docker image') {
	

	steps{
	script {
		app = docker.build("singabhm/train_app")
		app.inside {
			sh 'echo $(curl localhost:8080)'
			}
			}
		}
	}
stage('push docker image')
	{
	
	steps {
		script {
			docker.withRegistry('https://registry.hub.docker.com','DockerHub')
			{
				app.push("${env.BUILD_NUMBER}")
				app.push("latest")
			}
		}
	}
	}
           }
}
