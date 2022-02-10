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
				bat 'dotnet clean --configuration Release --nologo'
			}
		}

		stage('Install and Build') {
            environment {
                appVersion = "6.1.${env.BUILD_NUMBER}"
            }      
            stages {
                stage(".Net Core") {
                    stages {
                        stage('Restore Packages') {
                            steps {
                                bat 'dotnet restore "C:\projects\BEKK\bekk.JenkinsTest\bekk.JenkinsTest.WebApp"'
                            }
                        }
                        stage('Build') {
                            steps {
                                bat "dotnet build "C:\projects\BEKK\bekk.JenkinsTest\bekk.JenkinsTest.WebApp" --configuration Release -p:VersionPrefix=${env.appVersion} -p:InformationalVersion=${env.appVersion}"
                            }
                        }
                    }
                }               
            }
        }
	}
}