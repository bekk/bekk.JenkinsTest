pipeline {
	agent any
	stages {
		stage('Checkout') {
			steps {
				git(url: 'https://git.vegvesen.no/scm/timeplan/timeplan.git', branch: 'master')
			}
		}

		stage('Clean') {
			steps {
				bat '$dotnet clean --configuration $configuration --nologo'
			}
		}
	}
}