pipeline{
	agent any
	environment {
		version = "${env.BUILD_ID}"
	}
	stages {
		stage('fetch-code'){
			steps {
				sh '''
				cd /git-files/jenkins-docker-webpage/
				sudo git pull
				'''
			}
		}
		stage('build-image'){
			steps{
				sh '''
				cd /git-files/jenkins-docker-webpage/
				sudo ansible-playbook docker-build.yml --extra-vars "var=${version}"
				'''
			}
		}
		stage('deploy-image'){
			steps{
				sh '''
				cd /git-files/jenkins-docker-webpage/
				sudo ansible-playbook docker-deploy.yml --extra-vars "var=${version}"
				'''
			}
		}
	}
}
