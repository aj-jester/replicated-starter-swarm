pipeline {
    agent any

    environment {
	APP_VERSION = "0.5.0"
	REPLICATED_APP = "testing app slug"
	
    } 

    stages {

        stage('Test') {
            steps {
                sh 'echo "lgtm!"'
		sh "printenv | sort"
            }
        }

        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS'
              }
            }
            steps {
                sh 'curl -fsSL https://github.com/replicatedhq/replicated/releases/download/v0.10.0/replicated_0.10.0_linux_amd64.tar.gz | tar xvz'
		sh "cat replicated.yaml | ./replicated release create --promote Unstable --yaml - --version ${env.APP_VERSION} --release-notes \"Automated CI release for ${env.JOB_NAME} on build number ${env.BUILD_NUMBER}\""
            }
        }
    }
}
