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
				bat '${env.dotnet} clean --configuration ${env.configuration} --nologo'
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
                                bat '${env.dotnet} restore ${env.project_path}'
                            }
                        }
                        stage('Build') {
                            steps {
                                bat "${env.dotnet} build ${env.project_path} --configuration ${env.configuration} -p:VersionPrefix=${env.appVersion} -p:InformationalVersion=${env.appVersion}"
                            }
                        }
                        stage('Publish') {
                            steps {
                                bat "${env.dotnet} publish -r linux-x64 --self-contained false --configuration ${env.configuration} --nologo -p:VersionPrefix=${env.appVersion} -p:InformationalVersion=${env.appVersion}"
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
        dotnet = '/PROGRA~2/dotnet'
        project_path = '/projects/BEKK/bekk.JenkinsTest/bekk.JenkinsTest.WebApp/bekk.JenkinsTest.WebApp.csproj'
        configuration = 'Release'
        result_path = "${env.WORKSPACE}/bekk.JenkinsTest/bin/$configuration/net5.0/linux-x64/publish"
      }
}