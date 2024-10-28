node ('New-Appserver') 
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
          severity: 'high'
        )

	}

	
	stage ('BUILD-AND-TAG')
	{
		app = docker.build("johncollegeacc769/nodejs_2024")
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