pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Build stage'
            }
        }

        stage('Run Script') {
            steps {
                sh './hello.sh'
            }
        }

        stage('Verify') {
            steps {
                sh 'echo Pipeline completed successfully'
            }
        }
    }
}

