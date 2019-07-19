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
                sh 'make release'
            }
        }
    }
}
