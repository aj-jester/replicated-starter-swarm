pipeline {
    agent any

    environment {
	APP_VERSION = "0.5.0"
	REPLICATED_APP = "testing app slug"
	REPLICATED_API_TOKEN = "05e9c6fb226ff329ec91d2de26d72728453c9709f09cc5f3f2ec32262b2c7042"
    } 

    stages {

        stage('Fetch Replicated CLI') {
            steps {
                sh 'curl -fsSL https://github.com/replicatedhq/replicated/releases/download/v0.10.0/replicated_0.10.0_linux_amd64.tar.gz | tar xvz'
            }
        }

        stage('Deploy App via CLI') {
            steps {
		sh "cat replicated.yaml | ./replicated release create --promote Unstable --yaml - --version ${env.APP_VERSION} --release-notes \"Automated CI release for ${env.JOB_NAME} on build number ${env.BUILD_NUMBER}\" --app ${env.REPLICATED_APP} --token ${env.REPLICATED_API_TOKEN}"
            }
        }
    }
}
