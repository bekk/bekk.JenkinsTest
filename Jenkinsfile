pipeline {
	agent any
	stages {
		stage('Clean') {
		  steps {
			sh '$dotnet clean --configuration $configuration --nologo'
		  }
		}

		stage('build') {
			steps {
				sh 'node --version'
			}
		}

	}
}