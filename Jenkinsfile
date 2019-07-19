pipeline {
    agent any

    stages {

        stage('Test') {
            steps {
                sh 'echo "lgtm!"'
            }
        }

        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS'
              }
            }
            steps {
                sh 'curl -fsSL https://github.com/replicatedhq/replicated/releases/download/v0.10.0/replicated_0.10.0_linux_amd64.tar.gz | tar xvz -C deps'
            }
        }
    }
}
