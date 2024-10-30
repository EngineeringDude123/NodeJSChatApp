node ('Ubuntu-Appserver-3120') 
{
	def app	
	stage('CLONE GIT REPOSITORY')
	{
		checkout scm
	}

	stage('SCA-SAS-SNYK-TEST')
	{
		snykSecurity(
          snykInstallation: 'Snyk@latest',
          snykTokenId: 'SnykID',
          severity: 'critical'
        )

	}

	
	stage ('BUILD-AND-TAG')
	{
		app = docker.build("johncoll/nodejs_2024")
	}


	stage ('POST-TO-DOCKERHUB')
	{
		docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
		{
			app.push("latest")
		}
	}


	stage ('DEPLOYMENT')
	{
		sh "docker-compose down"
		sh "docker-compose up -d"
	}
	
}