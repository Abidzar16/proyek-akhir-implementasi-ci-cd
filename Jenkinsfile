pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deploy') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?'
                sh './jenkins/scripts/deliver.sh'
                sleep(time: '1 minute')
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}