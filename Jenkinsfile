pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                nodejs('Node') {
                    echo 'Building Application...'
                    sh 'npm install'
                }
            }
            stage('Test') {
                steps {
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
    }
}
