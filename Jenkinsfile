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
				bat '%dotnet% clean --configuration %configuration% --nologo'
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
                                bat '%dotnet% restore %project_path%'
                            }
                        }
                        stage('Build') {
                            steps {
                                bat "%dotnet% build %project_path% --configuration %configuration% -p:VersionPrefix=${env.appVersion} -p:InformationalVersion=${env.appVersion}"
                            }
                        }
                        stage('Publish') {
                            steps {
                                bat "%dotnet% publish -r linux-x64 --self-contained false --configuration %configuration% --nologo -p:VersionPrefix=${env.appVersion} -p:InformationalVersion=${env.appVersion}"
                            }
                        }
                    }
                }
            }
        }

        stage('Create Zip') {
          environment {
            resultFile = "${env.result_path}/bekk.JenkinsTest.WebApp-0.1.${env.BUILD_NUMBER}.zip"
          }
          steps {
            zip(zipFile: env.resultFile, dir: env.result_path, glob: '**/*')
          }
        }
	}

    environment {
        dotnet = 'C:\Program Files (x86)\dotnet\'
        project_path = 'C:\projects\BEKK\bekk.JenkinsTest\bekk.JenkinsTest.WebApp\bekk.JenkinsTest.WebApp.csproj'
        configuration = 'Release'
        result_path = "${env.WORKSPACE}/bekk.JenkinsTest/bin/$configuration/net5.0/linux-x64/publish"
      }
}