pipeline {
	agent any
	stages {
		stage('Checkout') {
			steps {
				git(url: 'https://github.com/bekk/bekk.JenkinsTest.git', branch: 'master')
			}
		}

		stage('Clean') {
			steps {
				bat '${dotnet} clean --configuration Release --nologo'
			}
		}
	}
}