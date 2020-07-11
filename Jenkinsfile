pipeline {
	agent {
		docker { image 'mcr.microsoft.com/dotnet/core/sdk:3.1-buster' }
	}
	stages {
		stage('build') {
			steps {
				sh 'dotnet --version'
			}
		}		
	}
}